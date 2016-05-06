---

title: Software Architecture ''ilities"
description:
tags: [list, software, architecture, functional, non-functional, requirements]
comments: true
image:
  feature: texture-feature-01.jpg
---

I recently posted another ‘Define’ article (this is where I expand on an acronym) based on NFR’s in which I mentioned the idea of software ‘ilities’. In software projects we must take into consideration ‘ilities’. Prioritising them is necessary because the client will inevitably demand that the project adheres to all of them (within reason).<br><br>

* Performance
	* How quickly must the system respond to interactive operations of different kinds?
	* Are there different classes of interactive operations that users have different tolerances / expectations for?
	* Is there a batch window? What runs in it?
	* Do the batches have their own performance constraints, e.g., to clear the batch window before it closes?
	* Does the batch load influence any interactive users running at the same time?
	* Is there data with a high read/write access ratio that can be cached in memory at different tiers in the architecture?
	* What are the expected performance bottlenecks?
		* CPU?
		* Memory on client, server or intermediate nodes?
		* Hard drive space on each node?
		* Communications links?
		* DB
		* Access
		* Searching
		* Complex joins
		* Interaction with other internal systems?
		* Interaction with systems in other departments?
		* Interaction with partner systems?
		* Interactions with public systems?
* Scalability
	* Peak load of how many users doing what kinds of operations?
	* Ability to grow to how many records in which critical database tables without slowing down related operations by more than X
	* Avoiding saturating a communication link that cannot be upgraded to a higher speed?
	* What dimensions can be scaled, e.g., more CPUs, more memory, more servers, geographical distribution?
	* Is the primary scaling strategy to “scale up” or to “scale out” — that is, to upgrade the nodes in a fixed topology, or to add nodes?
* Availability
	* What is the required up-time percentage?
	* Does this vary by time of day or location?
	* What is the current schedule of controlled outages? Is this acceptable, or is there a goal to improve it?
* Reliability
	* Are there components with reliabilities that are known to be less than the required reliability of the system?
	* What strategies are currently in place to build more reliable capabilities out of less reliable capabilities?
	* What is the expected mean time to failure by failure severity by operation?
	* How will reliability be assessed prior to deployment?
* Security
	* What operations need to be secured?
	* How will users be administered?
	* How will users be given permissions to access secured operations?
	* What are the different levels of security and how do these map
	* Security by operation
	* Security by type of object
	* Security by instance of object
* Maintainability
	* Are there concerns about the ability to hire appropriate technology skills, attract them to the area at reasonable prices?
	* What kinds of changes are anticipated in the first rounds of maintenance? What are their relative priority?
	* What sort of regression testing is required to ensure that maintenance changes do not degrade existing functionality?
	* What sort of maintenance documentation is expected to be produced? When?
* Flexibility
	* Is there system behavior that needs to be changed regularly without program changes?
	* Can this be encoded in the database?
	* Are there run-time rules that can be handled using a rules interpretation engine?
	* Are there functions that should be user scripted? If so, how will these be QA-ed?
* Configurability
	* What parameters need to be set on a machine-by-machine basis?
	* Personalizability
	* What aspects of the system can be customized on a per-user basis?
	* How does the user change these settings?
	* What is the strategy for defaults?
* Usability
	* Are there operations that need to be done as quickly as possible, so that user gestures should be minimized?>
	* Are there difficult or occasional-user operations that require non-standard presentations to help the user perform correctly?
	* What is the balance between data integrity and the ability to stop in a “work in progress” state?
	* What styles of validation are used in what situations?
	* What metaphors from existing or parallel systems should be used?
	* What sort of training deliverables are expected?
	* What sort of on-board help system is expected?
* Portability
	* Data portability between this system and other systems?
	* Portability across different versions of a single vendor’s DB?
	* Ability to port to a different vendor’s DB? Which one(s)? When?
	* Browser portability? What browser versions? Historical and future?
	* Operating system portability?
* Conformance to standards
	* What legal standards apply?
	* What technical standards apply?
	* Other standards, e.g., 508.1 for disabled users?
	* What development standards apply?
		* Database naming standards
		* Existing internal architectural standards (e.g., everything goes in an Oracle database)
		* Language and coding standards
		* Testing and review standards
		* Presentation standards, e.g., use of standard colors, controls or other affordance?
		* Lifecycle models or methodologies
* Internationalizability
	* What languages?
	* In what order?
	* How translated?
	* Single or multi byte character sets?
* Efficiency — space and time
* Responsiveness
	* What are the expected and upper limit response times per operation in the system?
	* What is the trade-off between lower averages and wider variations in response time?
* Interoperability
	* What systems will this system inter-operate with immediately?
	* What other systems are anticipated?
	* What classes of internal and external systems might later be needed to inter-operate with?
	* What functionality from this system needs to be exposed as a service in a service oriented architecture?
	* What functionality from this system needs to be exposed as a Web service or via a portal?
* Upgradeability
	* Do the servers need to be upgraded while running?
	* How many client stations need to be upgraded, and what are the costs and mechanisms for upgrading them?
	* How often do different kind of fixes need to be distributed? Are there “hot fixes” that have to go out right away, but others that can wait? How often do each kind occur?
* Auditability / traceability
	* What record of who did what when must be maintained?
	* For how long?
	* Who accesses the audit trails?
	* How?
	* Is archive to tape or other off-site storage media required?
	* Is “effective dating” required?
* Transactionality
	* What are the important database and application transaction boundaries?
	* Is standard “optimistic” locking appropriate, or is something more complex required in some or all cases>
	* Is disconnected operation required by any node?
	* Administrability
	* What live usage information needs to be displayed?
	* To who? How? When?
	* What “live” interventions are required?
	* What ability to handle remote configurations are required?
	* Are there existing application management consoles that will be used to manage this application?<br><br>

Phew, that was a list! Most of them are taken for granted and covered by good clean code and architecture. However some need to be seriously considered and implemented to ensure the project at hand runs smoothly throughout its life-cycle.
