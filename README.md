# cache_tests

This module contains python codes to generate assembly files for testing the data cache of the Chromite Core developed by [InCore Semiconductors](https://incoresemi.com/)

## Tests included
* Fill the cache completely based on the size mentioned in the core64.yaml input
* Try to fill the fill-buffer completely.
* Perform a load/store hit in the Fill-buffer
* Perform a replacement on all sets.
* Check if performance counters are correctly incremented.
## Test Logic
* ### uatg_cache_fillcache_01.py
     > * Clear the cache using fence operation.
     > * An arbitary value is loaded into t1
     > * A loop is run for as many times as is the size of the cache
     > * We do load operation inside each iteration of this loop,eventually filling up the cache
* ### uatg_cache_fillbuffer_01.py
     > * 
