# Process Best Practices

This is just an example of development process best practices. Different flows might require different rules.

# SCRUM

## Dailies (standups)

* Top to bottom review of all not-unstarted stories
  * At this stage stories can be marked as Delivered
* Discussing other issues not included in PT

## Iteration planning

### Prerequisites

* A day before
	* Each team member reviews potential tasks he will handle in next iteration
	* Ensures that each task has good quality description and acceptance criteria
	* Ensures that each task is tagged properly
	* ... then moves those tasks to iteration backlog
	* If necessary, developer can create new tasks as well

### Flow

* Dedicated person iterates through all unstarted tasks in iteration backlog
	* Verifies if description and acceptance criteria are in place. Reads those out loud.
	* Discusses unkowns etc.
	* Asks story owner for estimation

## Retrospective

### Prerequisites

* Each team member includes his concerns/thoughts/joys in dedicated document

### Flow

* Dedicated person iterates through all action items from previous retrospective
	* Obsolete action items are removed
* Dedicated person iterates through all retrospective entries
	* Reads those out loud
	* Entry owner clarifies his concerns/thoughts/joys
	* Action items are created if necessary


# Working with Pivotal Tracker

## General rules

* If possible, each team member should prioritize stories to the top of the list over those to the bottom of the list
* Each team member should ensure that only one of his tasks is in "started" state
* Every quarter Icebox should be cleaned (obsolete tasks should be removed)
* Whenever potentially obsolete task is spotted, it should be tagged with `drop` tag

## Flow

* Team member
	* Picks one of the tasks assigned to him, respecting task priorities (top to bottom)
	* Clicks start (story is now in `started` state)
	* Proceeds with any steps necessary to fulfill acceptance criteria
		* Provides updates in comments if possible
	* When acceptance criteria are fulfilled, clicks finish (story is now in `finished` state)
		* If applicable, PR should be created prior to finishing a story
		* If applicable, link to PR should be included in story comments
	* If any actions / changes are required, those should be taken care of
	* If applicable and if code (or other deliverable) is approved, story owner deploys code to staging or production environment 
	* Clicks "deliver" (story is now in `delivered` state)
	* If task needs to be verified by other team member, this team member should be added as an owner and mentioned in comment (requesting an acceptance)
	* Reviewer can accept or reject tasks during daily standup or immediatelly if possible
	* If task is rejected, it should be the top priority for story owner


## Types

* `Feature` - Default type. Any story that brings any kind of end-user oriented value should be of this type.
* `Bug` - Identified invalid behavior / error that needs to be fixed. 
* `Chore` - Task that does not bring any end-user oriented value (i.e. refactoring, code cleanup etc.). Try to avoid this type, and use features instead.

## Statuses

* `Unstarted` - nobody is actively working on this story
* `Started` - story is being deliverd by somebody (story owner is focusing on this particular story)
* `Finished` - story requirements have been fulfilled and story is now awaiting delivery (i.e. code review, deployment). If possible, story has been deployed on staging environment
* `Delivered` - story has been deployed to production environment and is awaiting final check
* `Accepted` - story is confirmed to be delivered successfully
* `Rejected` - deliverable does not meet all acceptance criteria and needs fixing. Story should be restarted by story owner.

## Tags

* All stories should be tagged with corresponding project name if possible
* If story belongs to an epic, it should be tagged with epic name
* Any story that is not a deliverable but is used to organize other tasks should be of `chore` or `release` type and tagged as an `idea`

## Estimating

* 0 - no effort (i.e. typo). Can take couple of minutes
* 1 - low complexity. Task is simple and is not a challange, needs little to no research etc. Usually can be completed in less than 2 days 
* 2 - medium complexity. Task is simple but might need some research and planning. Usually can be completed between 1-3 days
* 4 - high complexity. Task is challenging, requires research and planning with some unknowns. Usually can be completed between 1-4 days
* 8 - extreme complexity. Very complex task that cannot be included in iteration before splitting it into smaller stories.


## GitHub Labels

* `WIP` - work in progress, this PR does not need review yet
* `High Priority` - this PR requires prompt review
* `Merge after CI` - as reviewer, indicate that it is ok to merge this PR freely after CI is green
* `Merge after comments` - as reviewer, indicate that it is ok to merge this PR freely after owner reads up reviewer comments 
* `Merge after rebase` - as reviewer, indicate that it is ok to merge this PR freely after owner rebases this PR branch with master
* `Merge after squash` - as reviewer, indicate that it is ok to merge this PR freely after owner cleans up this PR commits history

## Definition of Done

### Before marking as PR Created

 **Keep sufficient quality**

* Code is tested properly and suite is :green_apple:
* Rubocop does not report any violations
* Obsolete commits are squashed/removed
* Integral code scattered between commits is squashed into single commits
* Basic refactorings are in place

### Before marking as Ready for QA

 **Make QA process smooth**

* Code is rebase-merged with master and pushed to heroku remote
* Successful deployment is ensured
* All necessary scripts are executed (i.e. migrations)
* All other prerequisites are applied (i.e. ENV variables)
* All correlated tasks are completed or scheduled (i.e. Setting up heroku scheduler entries)
* Feature is manually tested on production
* Task is investigated for requirements that might be not satisfied
* In case of complex nature of feature, testing instructions are provided in task update
