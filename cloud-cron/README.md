# Cloud Cron

## Use Case
On a set schedule a tenants workflow is executed.  The workflow could be as simple taking a snapshot of a VMs:   

	(30 08 * * * take-snapshots-of-everything)

The user should be able to see what cloud cron jobs/workflows have been configured for the specific tenants that they have access to through an API.

The status of current and past some number of past workflow executions should be persevered in the data model and available through the API

## Flow: 

* user schedules to run existing workflow
* workflow starts when scheduled time arrives

## Discussion
For more detailed example of snapshot based backup, see this [document](http://tinyurl.com/mhhvk89)
and [script](http://tinyurl.com/kybymjz) 

### Assumptions:

* Openstack action pack is an extensible set of actions (python scripts) that 
* Openstack pack configuration contains all specifics endpointns, etc. 
* Authentication and authorization is from Keystone integration, token is internally passed to the action: openstack actions take care of proper impersonation. 


### Question and answers:
