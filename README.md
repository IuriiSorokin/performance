# performance

If not considering computation-heavy applications, the usual bottlenecks are associated with memory access. This includes:
 * loading the data from RAM to CPU cache and from the cache to the registers.
 * reading the data from the file system (local or remote) or from a database into the RAM
 * memory allocation
 * copying and re-arranging the data in the RAM
 
Modern CPUs attempt to foresee what data is going to be accessed in the next instructions, and to pre-load it into the lower level cache or into the registers. Branches in various forms, such as `if` statements, virtual functions, function pointers, impede such possiblites. 

The general recommendation is that if one wants to speed-up an application, one should profile and identify the bottlenecks first, and not try to optimize here and there. Too often, figuratively, 80% of time is spent in 20% of the code, and for the other 80% of the code the optimizations are the root of all evil.

To identify the bottlenecks one can employ various techniques:
* use profilers, such as `callgrind`, `gprof`, or more advanced commertial products.
* randomly interrupt the execution (e.g. in `gdb`) and inspect the the stack. 
* embed the diagnostics into the application: dedicatedly measure the wall clock time spent in particular functions, or write the wall clock time and execution status into a log. 


In general, this is a very broad topic, and it very much depends on the application. 
