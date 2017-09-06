# General Notes
Search Method
- *Soundex* is a phonetic algorithm for indexing names by sound as pronounced in English. It is appropriate when you want to do name lookups and allow users to find correct results despite minor differences in spelling.

- *Fuzzy matching* is the technique of finding strings that match a string, approximately, not exactly. The closeness of a match is measured in terms of operations necessary to convert the string into an exact match.

- *Levenshtein*. It's a simple algorithm that provides good results, but it's not supported by MongoDB. Measuring the Levenshtein distance must thus be done by fetching the entire result set and then applying the algorithm for the search query on all the strings. The speed of the operation grows linearly with the number of documents in your database, so unless you have a very small document set, this is most likely not
worth doing

Website Documentation
http://patternlab.io/

# Reading list 
- Learning Scrapy
- Vagrant Virtual Development enviroment Cookbook
- Pro MERN stack
