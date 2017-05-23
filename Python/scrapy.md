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


# Issue
1. Blocking code will cause crawl failed or abnormal behaviour
