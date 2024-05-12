This is a templated class but as for the rest of the module, it doesn't need to be instanciated in any way. There will be one instance for each level of log. These can be used as the `std::ostream` class in C++, however, as this system isn't an overload of any kind of `std::ostream`, it won't work with `std::endl`, or any stream modifier in fact.

There is some basic modifiers and functors in a [[Proxy]] :
- `boolalpha` to print boolean values as `true` or `false` instead of `1` or `0`
- `noboolalpha` to revert `boolalpha`
- `flush` to end a log entry to the log [[Collector]].

[[Proxy]] instances are configured to be `thread_local` to move the need of synchronization from these instances to the Log [[Collector]].