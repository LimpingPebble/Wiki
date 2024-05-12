This is the only link to the log sink. It may be a file, or the console it self. It is the only part of this module that should be unique to a program.

To make it as fast as possible, it will be asynchronous, and will get its log entries from a circular buffer, it may result in the loss of some log entries if it isn't well configured, but this method reduces as much as possible the latency of logging.

This circular buffer is filled by [[Collector|collectors]] and read in the [[Stream]] instance. But as the [[Stream]] doesn't have a way to know that there is new entries, it will regularly clear the buffer and dump its content to its sink.

There is two main settings to consider:
1. The maximum size of the circular buffer 
	- if it is too small we may lose a lot of logs
	- if it's too big, it's a loss of storage, which isn't wanted
2. The frequency at which we clear the circular buffer
	- If it is too big, the circular buffer will have time to fill up.
	- If it is too small, the thread will become an intensive task and start monopolizing CPU's resources, again, it isn't wanted.
	