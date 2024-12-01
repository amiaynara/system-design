## Notes


### Proxies
**Proxy:** An entity that intercepts communication __on behalf__ of another entity(machine) in a system.
**Forward Proxy:** A machine on the client side makes the request on the behalf of the client (curtailing the identity of the client)[handles outbound requests]
**Reverse Proxy:** A machine on the server side intercepts the request on the behalf of the server (curtailing the identity of the server)[handles inboud requests]

#### Can one server behave as a forward as well as a reverse proxy? Think why or why not?
- Yes.  


### Thick and Thin clients
**Thick clients**: The system which has most of the logic on the client side
**Thin clients**: The system which has most of the logic on the server side

#### List down the real world use cases when you would choose a thick client architecture over thin client architecture and vice versa. List pros and cons in all scenarios. Can you think of a system which has thick client and thin client and multiple tiers? Also, can servers behave as clients?
- Video Editing software is thick client architecture design
- Aws console is thin client, facebook is thin(?)
- Addition of cache, LBs leads to architecture being multi-tier

### Data & Dataflow
* If we think about it, user interacts with the system through data.
* This data is in different forms at different layers
	* Business layer: Images, text
	* Application layer: JSON, XML
	* Database layer: tables, indices, graphs, lists
* If we remove data from the scene, there is nothing really that is interesting.
* While designing system, I need to think about the:
	* type of data
	* the volume of data

#### Relational Database
- If I can ensure that I need a column which stores the data where a field cannot be null, or specify a constraint
- If ACID property is needed
	* **Atomicity** of transactions (a set up read or write operations either completes or does not complete)
	* **Consistency**: Two reads at an instant must read **the same value**
	* **Isolation**: Two transactions should not know about each other
	* **Durability**: Data should get stored permanently if the transaction is successfull
- if schema is relatively fixed
	* JOINS become expensive for queries
	* schema updation is complex
- easy to **scale vertically**
- horizontal scaling is difficult
- 
- 

#### Non-relational
##### KV stores
	* keypair values
	* city: feature data
	* request: response
	* fast and in-memory store
##### Document based
	* when not sure about schema (evolve over time)
	* heavy reads and writes
	* **collections and documents** 
	* highly scalable
	* sharding
	* dynamic data flexibility
	* special query operations / aggregation
##### Column DBs
	** needs more clarity **
	* heavy reads (like songs streaming), special writes
	* 

##### Search DBs
	* not the primary data store
	* data is stored in the form of indices
	* these act as a middleman between reads and the primary data store (rel or non-rel)


### Applications/Services
Analogy: Functionalities of a building(the system): elevator, electric supply, water supply.
Applications/services are pieces of codes that run on machines to fulfill certain task. There might be more than one machine
present and they could be spread geographically. This implies that the need for communication has to be thought out well, and
is a part of the design.

#### Types of apps
**Client Apps**:
	* Usually the piece of code that the users of the services/functionality interact with
	* 
**Backend Apps**:
	* the apps that is placed at a centralized location which can serve requests from various clients
	* There can be one or more pieces of applications/services that forms that backend

##### Factors to consider while designing a system
	* requirements
	* Layers
	* tech stack
	* code structure/design patterns
	* data store
	* performance/cost
	* deployment
	* monitoring
	* reliability

Think of an application that is supposed to solve the parking location problem.
	* requirements
		* how big is the parking lot
		* what is the map of the parking lot (? is this really necessary ?)
		* what is the capacity
		* how many spots are empty at a given time
		* what is the next empty spot
		* what is the cost of parking
		* what is the business rule for payment
		* are we looking to replace any and all human in the process
	* Layers
		* should be a CLI? yes i think we might get away without frontend if there are no security personnel. the security personnel who will be using the application are not used to this
		* A frontend service is required (??)
		* A backend that handles payment
		* A backend app that handles the registering and finding out the next empty spot
		* A frontend application that takes a picture of the car plate number
		* A backend service to run AI algorithm to digitise the car plate number
	* tech stack
		* command line interface (linux base os on the frontend)
		* A linux server on the backend python (for image processing, opencsv)
		* third party payment gateway or integration of fast-tag
		* the microcontrollers to open and close gates and all other required embedded systems
	* code structure/design patterns (?? not sure ??)
	* data store
		* relational database(we can design the schema, looks not very complicated on the first look) aws rds
		* aws s3 to store the vehicle numbers for future references and logging
		* 
	* performance/cost
		* generation of vehicle number should not be very time intensive, should be quick (using AI)
	* deployment
		* large number of parking spots in the city, so deplyment should be automated and easilty manageable
	* monitoring
		* proper logging, since it involves daily lives of the public
		* data can be required to resolve any issues (legal/medical...)
	* reliability
		* generation of vehicle number should reliable
		* the payment gateway should be reliable
		* the opening and closing of gates should be reliable


### APIs
Interface through which one piece of code interacts with another piece of code.
OS exposes some APIs for users or linux programs to so that they can also have access to some information which they usually don't have.
Similarly any application can expose APIs so that other applications can interact and send and receive data.
	* Abstraction
	* Communication
	* 
Examples: Private APIs, Public APIs, Web APIs, SDK/Lib API
Factors:
	* API Contracts
	* Documentation
	* Data formats
	* Security

#### Standards	
##### RPC
	* 
##### SOAP
	*
##### REST

### Caching
#### Cache-aside pattern
#### read-through pattern (for read heavy)
#### write-through pattern (write heavy)
#### write back pattern (write a batch to the cache(that sits between app and db) and later cache will write to the db)

### REST APIs
- Guidelines:
* 

These are used by REST to implement the CRUD operations: POST, PUT, GET, OPTIONS, PATCH, DELETE
Security of REST APIs must be taken care of as well.
Throttling: When all requests are not handled
Rate limiting: Limiting the number of requests that an api can handle.


### Message Queues

#### Messages
* “decoupling”
* Any changes made to one application doesn’t affect other application as long as communication contract is not breached
* We can break one monolith application into smaller applications which reduces overall complexity.
* It becomes easier to maintain and debug applications.
* We can have cross platform applications. Smaller applications can be independently developed in any programming languages and scaled.

- Message queues is a concept that tries to solve the problem of asyncronous communication.
- **Producer** produces messages (some data/information) that need to be further processed, but the results do not have to instanteneous.
Client could produce a message or a another backend service could produce a message for the consumer to process.
- based the load we can tweak the number of consumers
#### Order
Depending up on the use case the order may or may not matter. If it is FIFO, then in case of a failure while consuming or if the consumer does not
acknowledge the consumption. If the consumption fails for a message, then the whole consumption stops for FIFO (be it one consumer or multiple consumers).
#### Consumption
If consumption fails, (order does not matter) then message is pushed to a **dead** queue and then retried.

#### Publish-Subscribe (reminds me of the pattern- subject-subscriber pattern)
* There is an entity that broadcasts the messages and then there are others **subscribe** to it.
Imagine a hospital (Dr. House), where there are interns, experts, surgeons, staff (basically different groups). Hospitals generally have a broadcast system.
A pager system to reach the individuals separately. Now what usually happens is that not every personnel is notified with each message. It is more efficient
to send messages to only those who are concerned. And also it necessary to make sure that message prompty received in case of emergency.
So solve this problem, people are classified in to groups. And then each of these groups can subscribe to a particular **topic**.

How it might look like ->
```
		
			PUBLISHER -> input channel		(message broker)        	output channel  - s1
												s3, s4, s2 ... sn


```
*Note*:
* A subscriber need not be a user (who receives a mail or sms). A subscriber can be anything. A service (hence there can be a group of services subscribed
to a particular topic).
* This makes our system much more scalable and provides a granular control over the parts which can be scaled
* Message ordering: order of message (often not required, but we must think of it before using using this pub-sub pattern) 
* Poison messages: when using third party publishers, we have to be sure make sure that we are properly handling any malicious messages
* Duplicage messages: it has to be made sure that same message is not read twice or more.

