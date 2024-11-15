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

