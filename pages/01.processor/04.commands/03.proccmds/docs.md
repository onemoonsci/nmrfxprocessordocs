##Processor Commands##

The actual sequence of processing operations is automatically parallelized and run on multiple processing cores.  For example, a MacBook Pro might have an Intel i7 processor with 4 cores.  Each of those cores is "hyperthreaded" so in total the CPU appears to the operating system (and the Java code of NMRFx) as if it can run 8 simultaneous operations.  The sequence of operations would therefore be replicated 8 times, and each sequence would get a subset of the total vectors that need to be processed.  The commands in this section allow the user to override the default setup and explicitly specify the number of "simultaneous" processes to run, and what size chunk of vectors they should each grab.


**procOpts** 

Set and get various options in the Processor


    procOpts(nprocess=None,nvectors=None)

* **nprocess**
The number of processes to run simultaneously.  Defaults to number of cpu cores (x2 with hyper-threaded)
    * *default* None
    * *optional* True
* **nvectors**
The number of vectors each process should grab at one time.
    * *default* None
    * *optional* True

**run** 

Execute the series of operations that have been added to processor. Return true if it executed successfully. The run command must be present at the end of processing operations or no processing will happen.


    run(process=None)

