# performance

If not considering computation-heavy applications, the usual bottlenecks are associated with memory access. This includes:
 * loading the data from RAM to CPU cache and from the cache to the registers.
 * reading the data from the file system (local or remote) or from a database into the RAM
 * memory allocation
 * copying and re-arranging the data in the RAM
 
In multi-threaded, multi-process, and multi-component applications the performance can also be inhibited by interdependencies, and concurrency for a resource (again, usulally IO).

The general recommendation is that if one wants to speed-up an application, one should profile first, and not try to optimize here and there. Too often, figuratively, 80% of time is spent in 20% of the code (in fact the ratio can be much more drastic), and for the other 80% of the code the optimization is the root of all evil.

To identify the bottlenecks one can employ various techniques:
* use profilers, such as `valgrind`, `gprof`, or more advanced commertial products.
* randomly interrupt the execution (e.g. in `gdb`) and inspect the the stack. 
* embed the diagnostics into the application: dedicatedly measure the wall clock time spent in particular functions, or write the wall clock time and execution status into a log. 
* profile the resource utilization: CPU load, various IO including cache misses, memory allocation from the OS. 

Some basic considerations on how to avoid performance overhead: 

* Avoid data copying.
* Use dynamic memory allocation only when appropriate, and only as much as necessary. Use `reserve` and similar functions. Consider re-using allocated memory (make local object a member). Consider using custom allocators.
* Facilitate compiler optimiaztions: keep simple functions in headers, so they can be inlined; pass by value when appropriate (for RVO and copy ellision); don't abuse `const` (can prevent from moving);
* Facilitate CPU caching: use small objects, consider alignment of the member variables, prefer lazy evaluation.
* Avoid branches (`if` statements, virtual functions, function pointers).
* Consdier using `float` instead of `double`. 

In general, this is a very broad topic, and it very much depends on the application. 
