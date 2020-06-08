# Event Loop and Request Animation Frame

* Tasks: run in a queue (fifo). One task per event cycle loop after the synchronous tasks are executed. If additional tasks are queued during this execution, then this new ones are executed as well. This mean that they can block execution of the main thread.
* Request Animation Frame: Run in a queue fashion. Every task already in the queue in the current frame are executed. Additional requests added during the current frame are delayed until the next frame.
