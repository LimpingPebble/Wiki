This module regroups classes to manage logs. Users will use instances of the [[Proxy]] class to send logs to a [[Collector]] instance, finally this collector will dump logs to the [[Stream]] instance.
- Almost all classes in this module can't be instantiated, copied or moved.
	- This implies that the state of this module will generally be the same for the whole program.
- This module should be standalone, and should be used as is, without any overloading or external dependency (except Boost and the system's library).
- No special registration or allocation should be performed by any user code, if any is needed, it should be viewed as a bug.


This whole system will generate and convey log entries from the basic user input to the end where these entries should be dumped to the log sink. Log entries consist of at least a `time_point`, a `level`, a location (`filename` and `line`), and finally a message which may use multiple lines.

The `Levels` it accept are
1. `TRACE`
2. `DEBUG`
3. `INFO`
4. `WARN`
5. `ERROR`
6. `FATAL`
7. `OFF`
`Levels` values should be considered as minimum levels, so following this logic, to disable logging, [[Collector|collectors]] should be set to the level `OFF`, the only level without a [[Proxy]].