# Scrapy notes


### Important notes
1. Python twisted
2. Using MySQL instead of MongoDB due to some of the drawbacks that when using MongoDB as Database for data scraping.
3. Using large pool of IP (proxy) to route requests
4. Increasing request delay
5. Reduce number of requests per second


### A table that can help you decide what the best mechanism for a given problem is:

| **Problem**        | **Solution**           |
| ------------- |:-------------:|
| *Something that is specific to the website that I'm crawling.*   | `Modify your Spider.` |
| *Modifying or storing Items—domain-specific, may be reused across projects.*     | `Write an Item Pipeline.`      |  
| *Modifying or dropping Requests/Responses—domain-specific,may be reused across projects* | `Write a spider middleware.`|
| *Executing Requests/Responses—generic, for example,to support some custom login scheme or a special way to handle cookies.* | `Write a downloader middleware.`|
| *All other problems.* | `Write an extension.`|


# Performance
1. Find the bottleneck
2. lantencies: t(download) = t(response) + t(overhead) 
    - t(job) = (N(request) * (t(response) + t(overhead))) / CONCURRENT_REQUESTS + t(start/stop)
3. Parameters control
    - t(overhead): more powerful server
    - t(start/stop) : same as above

4. Caculate the throughput 
    - T = N/(t(job) - t(start/stop))
    - By running a long job of N Requests, we can measure the job t aggregated time and then it's straightforward to calculate T.


## Case study:
### 1. saturated CPU
**Solution**: I will assume that your code is, in general, efficient. You can get
aggregated concurrency larger than *CONCURRENT_REQUESTS* by running many Scrapy
crawlers on the same server. This will help you utilize more of the available cores
especially if other services or other threads from your pipelines don't use them.
If you need even more concurrency, you can use multiple servers (see Chapter 11,
Distributed Crawling with Scrapyd and Real-Time Analytics), in which case you will
likely have more memory, network bandwidth, and hard disk throughput available
as well. Always double-check that CPU usage is your primary constraint.

### 2. blocking code
**Solution**: I will assume that you inherited the code base, and you have no intuition
on where the blocking code is. If the system can be functional without any pipelines,
then disable your pipelines and check whether the odd behavior persists. If yes, then
your blocking code is in your spider. If not, then enable pipelines one-by-one and
see when the problem starts. If the system can't be functional without everything
running, then add some log messages on each pipeline stage (or interleave dummy
pipelines that print timestamps) in between your functional ones. By checking the
logs, you will easily detect where your system spends most of its time. If you want
a more long-term/reusable solution, you can trace your Requests using dummy
pipelines that add timestamps at each stage to the meta fields of Request. At the end,
hook to the item_scraped signal and log the timestamps. As soon as you find your
blocking code, convert it to Twisted/asynchronous or use Twisted's thread pools. To
see the effects of this conversion, rerun the previous example while replacing SPEED_
*PIPELINE_BLOCKING_DELAY* with *SPEED_PIPELINE_ASYNC_DELAY*. The change in
performance is stunning.

### 3. "garbage" on the downloader
**Solution**: We can solve this problem using treq instead of *crawler.engine.
download().* You will note that this will skyrocket the scraper's performance, which
might be bad news for your API infrastructure. I would start with a low number
of *CONCURRENT_REQUESTS* and increase gradually to make sure I don't overload the
API servers.

### 4. overflow due to many or large responses
**Solution**: There isn't much you can do for this problem with the existing infrastructure.
It would be nice to be able to clear the body of Response as soon as you don't need it
anymore—likely after your spider, but doing so won't reset Scraper's counters at the
time of writing. All you can really do is try to reduce your pipeline's processing time
effectively reducing the number of Responses in progress in the Scraper. You can
achieve this with traditional optimization: checking whether APIs or databases you
potentially interact with can support your scraper's throughput, profiling the scraper,
moving functionality from your pipelines to batch/postprocessing systems, and
potentially using more powerful servers or distributed crawling.

### 5. overflow due to limited/excessive item concurrency
**Solution**: It's very easy to detect both problematic symptoms of this case. If you
get very high CPU usage, it's good to reduce the number of CONCURRENT_ITEMS. If
you hit the 5 MB Response limit, then your pipeline can't follow your downloader's
throughput and increasing CONCURRENT_ITEMS might be able to quickly fix this. If it
doesn't make any difference, then follow the advice in the previous section and ask
yourself twice if the rest of the system is able to support your Scraper's throughput.

### 6. the downloader doesn't have enough to do
**Solution**: If each index page has more than one next page link, we can utilize them
to accelerate our URL generation. If we can find pages that show more results (for
example, 50) per index page even better. 

## Troubleshooting flow
To summarize, Scrapy is designed to have the downloader as a bottleneck. Start with
a low value of CONCURRENT_REQUESTS and increase until just before you hit one of
the following limits:
- CPU usage > 80-90%
-  Source website latency increasing excessively
- Memory limit of 5 Mb of Responses in your scraper

At the same time also perform the following:
- Keep at least a few Requests at all times in the scheduler's queues (mqs/dqs)
to prevent the downloader's URL starvation
- Never use any blocking code or CPU-intensive code

![Troubleshooting Scrapy's performance problems](https://octodex.github.com/images/yaktocat.png)
