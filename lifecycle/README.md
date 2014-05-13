# Lifecycle management

## Use Case
As a means to manage capacity we would like to enforce a lease on all non-production resources.  The workflows that manage the lease will provide notifications (emails, etc) to the user as well as provide them with the means to renew their leases a given number of times.

Through an API the user should be able to query the state of their existing leases.

Through an API the user should be provided with the ability to renew their lease.

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
