# Scrapy notes


### Important notes
1. Python twisted
2. Using MySQL instead of MongoDB due to some of the drawbacks that when using MongoDB as Database for data scraping.
3. Using large pool of IP (proxy) to route requests
4. Increasing request delay
5. Reduce number of requests per second


### A table that can help you decide what the best mechanism for a given problem is:

| Problem        | Solution           |
| ------------- |:-------------:|
| Something that is specific to the website that I'm crawling.   | Modify your Spider. |
| Modifying or storing Items—domain-specific, may be reused across projects.     | Write an Item Pipeline.      |  
| Modifying or dropping Requests/Responses—domain-specific,may be reused across projects | Write a spider middleware.|
| Executing Requests/Responses—generic, for example,to support some custom login scheme or a special way to handle cookies. | Write a downloader middleware.|
| All other problems. | Write an extension.|


There must be at least 3 dashes separating each header cell.
The outer pipes (|) are optional, and you don't need to make the
raw Markdown line up prettily. You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3
