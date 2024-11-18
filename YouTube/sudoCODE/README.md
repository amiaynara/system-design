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
