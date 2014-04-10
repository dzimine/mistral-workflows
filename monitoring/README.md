# Lifecycle management

## Scenario One


## Scenario Two
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
                for memory consumption type problems – stop and restart identified processes
                for hung process type problems – stop and restart identified processes
                for deadlock type problem – fix deadlocks
  * output:
     all repairs should be self-testing to verify successful completion or not
                success or non-success
                causing a retest of the reporting condition (the initial monitor)
                if monitor does NOT turn green, then move to next problem-type + target(s)
 
                                     if at end of all attempts for automated repair, the underlying condition has not changed, notify a human



## Original Flow:

* User creates a VM
* By listening for a Nova “create virtual machine event” a lease workflow is started
* User is notified of lease creation 
* At some X time before lease expires a notification providing on option to extend the lease
* Option is presented if lease qualifies (hasn’t met extension cap for example)
* Lease expires by exceeding configured duration
* All resources related to the VM are backed up and then destroyed 
* During the life of the lease the user or a delegate should be able to extend the lease.

## Modifyed Flow

* provision command triggers 'lease VM workflow'
* user is notified of lease creation
* at lease expiration, user is notified, with an option to extend the lease
* The user can extend the lease up to N times.
* if user doesn't respond with request for extention within X hours, the VM is decomissioned.
* at lease 
* vm provision and vm decomission are the separate flows. 
* revive VM from a backup by user request may be yet another flow. 


## Discussion

* The better alternative may be to watch the lease from event scheduler and trigger appropriate workflows on lease expiration or lease extension events. 

    * TODO: write event based lease workflow



### Assumptions:

### Question and answers:

# Credits
* Jay Hahn-Steichen at intel.com
