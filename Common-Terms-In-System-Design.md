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

### 7. Rate Limiting  

- Prevents a single user from making too many requests too fast, ensuring fair usage for everyone.  
- Just like a coffee shop limiting customers to two free refills, it helps prevent API abuse and denial-of-service attacks.  

### 8. Stateful vs. Stateless Systems

- Stateful System: Maintains data between requests (like remembering your login session on a website).
- Stateless System: Doesn’t retain data between requests (like a vending machine that serves each user independently). Stateless systems are easier to scale in distributed environments.



  

