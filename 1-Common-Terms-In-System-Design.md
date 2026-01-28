 #### 1. Scalability  

- The ability of a system to handle increasing workloads efficiently. There are two types:  

- Horizontal Scaling: Adding more machines (like hiring more employees in a factory) to share the load.  

- Vertical Scaling: Upgrading existing machines (like giving an employee better tools) to handle more work.  
 
- A good system should be designed with scalability in mind to prevent bottlenecks as demand grows.  

#### 2- Throughput  

- The number of requests a system can handle per second. Think of it like how many customers a store can serve at once.  
- High throughput is essential for applications with large user bases, like social media platforms.  

#### 3. Latency  

- The time it takes for a request to travel from the user to the system and back. Lower latency means faster responses.  
- Reducing latency improves user experience, especially for real-time applications.  

#### 4. Load Balancing  

- Distributes incoming requests across multiple servers so that no single machine gets overloaded. Think of it like multiple checkout counters in a supermarket, ensuring that customers (requests) don’t have to wait too long.  
- Load balancers can work at Layer 4 (transport layer) or Layer 7 (application layer) of the OSI model.  

#### 5. Caching  

- Stores frequently accessed data temporarily so it can be quickly retrieved without needing to recompute or fetch it again. Imagine saving your favorite playlist offline instead of streaming it every time.  
- Caching helps reduce database load and improves response times.  

### 6. API Gateway  

- Acts as a traffic controller for APIs, deciding which requests go where and ensuring smooth communication between services. Similar to a receptionist directing visitors to different offices.  
- API gateways also provide security features like rate limiting and authentication.
- We can do Rate Kimiting in API gateway.   

### 7. Rate Limiting  

- Prevents a single user from making too many requests too fast, ensuring fair usage for everyone.  
- Just like a coffee shop limiting customers to two free refills, it helps prevent API abuse and denial-of-service attacks.  

### 8. Stateful vs. Stateless Systems

- Stateful System: Maintains data between requests (like remembering your login session on a website).
- Stateless System: Doesn’t retain data between requests (like a vending machine that serves each user independently). Stateless systems are easier to scale in distributed environments. we use Token to again login back to system.  

### 9. Database Sharding  

- Splits a huge database into smaller, more manageable pieces so that queries run faster. Similar to dividing a school into multiple classrooms instead of cramming all students into one room.  

- Sharding helps improve database performance and horizontal scalability.  

### 10. Replication  

- Makes copies of important data in multiple places so it's safe if one copy is lost. Similar to having multiple backups of your important documents.  

- Replication ensures high availability and fault tolerance.  

### 11. Event-Driven Architecture  

Triggers automatic actions when something happens, like a doorbell ringing when pressed or an email notification when you receive a message.  

This architecture helps decouple services and improves responsiveness.  
  
### 12. Message Queue  

Stores tasks in a queue and processes them one by one, ensuring no request is lost. Similar to waiting in line at a school cafeteria.  

Message queues help in building scalable and fault-tolerant systems.  


  

