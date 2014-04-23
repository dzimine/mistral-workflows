# Making Monitoring Actionable

## Scenario One - high memory usage on mysql server

#### Monitor
* mysql monitoring
* discovers memory usage above 90%  (trigger that initiates workflow)
#### Diagnostics
* input: 
  * from perfmon on windows;  could be a run-time query but probably from data warehouse
  * from top on linux; could be a run-time query but probably from data warehouse
    * verify memory leak trend 
      * (are there leaks, how rapidly did we get here, how long have been here)
      * (is it a DB infrastructure issue, or a leak from the application?)
  * check top memory consuming processes
  * check for hung processes
  * check for deadlocks in mysql
* output:
  * identify the top candidate for repair action  (a ranked list of targets for repair)
  * problem type (a ranked list of problem types to repair)

#### Repair
  Do one type of repair at a time, then retest the underlying condition, if not fixed, continue to next repair
  
  * input:
		* a ranked list of problems
		* identity of candidate(s)/target(s) and type of problem (output from diagnostics)       
		* for memory consumption type problems – stop and restart identified processes
		* for hung process type problems – stop and restart identified processes
		* for deadlock type problem – fix deadlocks
  * output:
     			
		all repairs should be self-testing to verify successful completion or not        
	* success or non-success
	* causing a retest of the reporting condition (the initial monitor)
	* if monitor does NOT turn green, then move to next problem-type + target(s)
	* if at end of all attempts for automated repair, the underlying condition has not changed, notify a human

## Scenario Two - disk filling on a server
 
 
### Monitor

* disk space monitoring
* discovers disk space usage above 90%  (trigger that initiates workflow)

### Diagnostics
input: 

* perfmon collects free disk space; run-time or datawarehouse
* df on linux collects free disk space; run-time or datawarehouse

actions:

* windows – system drive or non-system drive
* identify candidates for removal via black-list
* calculate how much disk space will be released by removal of files
* check trend (how far am I over threshold, how fast did I get here, etc.)
* check with capacity management to see if disk can grow

output:

* result from checks (files to remove, space to be recovered, trend, capacity data)

### Repair
do one type of repair at a time, then retest the underlying condition, if not fixed, continue to next repair

input:

* from diag output the problem types + target(s)

actions:

* remove files specified
* make request of capacity mgt to grow disk
* split DB files

output:

	all repairs should be self-testing to verify successful completion or not
* success or non-success
* causing a retest of the reporting condition (the initial monitor)
* if monitor does NOT turn green, then move to next problem-type + target(s)
* if at end of all attempts for automated repair, the underlying condition has not changed, **notify a human**

## Discussion

* Jay: "We need an easy way to add/remove diagnostic and repair steps.  A standard way of referencing the “type” of a problem found by monitoring and by diagnostics needs to be fleshed out – we know of no industry specification here.   A way to identify the probable next step from a list of possible steps would be a cool feature (e.g. diagnostics returns 4 possible problem types, instead of trying them FIFO or alphabetically – they could be weighted by past success ratios and try the most successful first).  We anticipate that there is an API for the monitoring system to which the test requests could be sent and a result returned."
 
### Assumptions:

### Question and answers:

# Credits
* Jay Hahn-Steichen at intel.com
