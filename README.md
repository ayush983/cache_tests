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
     > * A loop is run for as many times as is the size of the cache
     > * We do load operation inside each iteration of this loop,eventually filling up the cache
* ### uatg_cache_fillbuffer_01.py
     > * Clear the cache using fence operation.
     > * A loop is run for as many times as is the size of the cache
     > * We do load operation inside each iteration of this loop,eventually filling up the cache
     > * A series of 70 nops is done to clear the fill buffer.
     > * A loop is run for 10 more times than is the size of the fill buffer.
     > * We do load operation inside each iteration of this loop,eventually filling up the fill buffer.
* ### uatg_cache_hitfb_01.py
     > * Clear the cache using fence operation.
     > * A loop is run for as many times as is the size of the cache
     > * We do load operation inside each iteration of this loop,eventually filling up the cache 
     > * Clear the fill buffer using a series of 30 nops.
     > * Fill the fill buffer partially using load operations.
     > * Run the loop to create hits on the fill buffer by decrementing the address each time.
* ### uatg_cache_setrepl_01.py
     > * Clear the cache using fence operation.
     > * A loop is run for as many times as is the size of the cache
     > * We do load operation inside each iteration of this loop,eventually filling up the cache
     > * A series of 70 nops is done to clear the fill buffer.
     > * A loop is run for 10 more times than is the size of the fill buffer.
     > * We do load operation inside each iteration of this loop,eventually filling up the fill buffer.
     > * Perform more load operations,creating a miss each time,resulting in replacement in the cache.
     > * The address is incremented such that each iteration performs a replacement on a different set.
* ### uatg_cache_perfcounter_01.py
     > * Loading the value of cache size in t3
     > * Doing load operations to fill up the cache and generating a miss each time
     > * Checking the number of write accesses to the cache using mhpmcounter17 and comparing it with value in t3
     > * Number of write acceses should be as many as is the size of the cache
     > * Generating hits on the cache as many times as is the size of the cache.
     > * Comparing the value of mhpmcounter16 to the value in t3.Each hit will result in read access to the cache
