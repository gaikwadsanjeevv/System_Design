# System Design  
Concepts aims to build systems that are reliable, effective, and maintainable.  

- System design borrows many great concepts from distributed systems. Apart from distributed systems, some basic concepts on computer networking and operating systems are also helpful before taking this course.  

## distributed system  
- A distributed system is a system whose components are located on different networked computers, which communicate and coordinate their actions by passing messages to one another.  
![image](https://github.com/user-attachments/assets/88b0b155-2a48-41ec-9956-95f33c734608)  
- Performance is the degree to which a software system or component meets its objectives for timeliness.  
- Scalability is the capability of a system, network, or process to handle a growing amount of work, or its potential to be enlarged to accommodate that growth.  
  - If we build a distributed system, we can split and store the data in multiple computers, and distribute the processing work.  
    - Vertical scaling refers to the approach of scaling a system by adding resources (memory, CPU, disk, etc.) to a single node. Meanwhile, horizontal scaling refers to the approach of scaling by adding more nodes to the system.  
- Availability is the probability of a system to work as required, when required, during a mission.  
- Redundancy is one of the widely used mechanisms to achieve higher availability. It refers to storing data into multiple, redundant computers. So, when one computer fails, we can efficiently switch to another one. This way, we’ll prevent our customers from experiencing this failure.  

- To help Developers build better systems, Scientists created a collection of false assumptions.  
![image](https://github.com/user-attachments/assets/67e62a6c-2456-471d-b360-a15f9e6b664f)  
- **Network asynchrony**, **partial failures**, and **concurrency** are the major contributors to complexity in the field of distributed systems, making distributed systems challenging.

- We can define the correctness of a system in terms of the properties it must satisfy.
  - Safety property  
  - Liveness property  
  There are some problems that make it physically impossible to satisfy both kinds of properties. So, we need to compromise some liveness properties to maintain safety.

- we need a common framework to solve problems generically Making a generic model  
- To create a model of a distributed system, we must define several properties it must satisfy. If we prove an algorithm is correct for this model, we can be sure that it’ll also be correct for all the systems that satisfy these properties.

- The **main important properties in a distributed system** concern the following:  
  - How the nodes of a distributed system interact with each other  
  - How the nodes of a distributed system can fail  
- **Categories of distributed systems**  
 - Synchronous systems- all nodes run in lock-step.  
 - Asynchronous systems- all nodes run at independent rates, there is no fixed upper bound on how long it takes for a node to deliver a message.
   - Note: The asynchronous model is closer to real-life distributed systems
### Common Types of Failures.  
![image](https://github.com/user-attachments/assets/b661698f-daa8-42b8-a104-bec9fe104ee7)  
- In **Fail-Stop** - node remain halted permanantely and other node detects it.
- In **Crash** A node halts, but silently. So, other nodes may not be able to detect this state. It can only identify when they communicate with it.
- In **Omission** A node fails to respond to incoming requests.
- **Byzantine failures**q occur when a node does not behave according to its specific protocol or algorithm. This usually happens when a malicious actor or a software bug compromises the node.  

### Exactly-Once Semantics  
- Multiple deliveries of a message: There might be a case for sending multiple messages due to network issue, but it could be a problem when it comes to bank trasfers, one bank may charge twice.
   - To avoid such situation we have to use approach where the node process the message only one time. though it may be delivered multiple times.
   - We can use Idempotent Operation- No matter how many times you perform the operation (once or 100 times), the end result is exactly the same as if it were performed once.
      - RESTful design treats a PUT request as idempotent.  
 ![image](https://github.com/user-attachments/assets/6dc368bb-a776-40dc-a143-8c55d7dbd1d7)  

![image](https://github.com/user-attachments/assets/762548da-4e1f-4cd9-a4f9-760677574414)  
![image](https://github.com/user-attachments/assets/f63f7da1-62b4-4e1a-83e2-e614a369e206)  

### ✅ De-duplication (Simple Explanation)  
In the de-duplication approach, each message has a unique ID.  
If the same message is sent again (retried), it will still have the same ID.  
The receiver checks if it has already processed that ID.  
If yes, it skips processing again.  
This avoids duplicate actions like sending the same email multiple times.  

📌 Important  
Sender creates the unique ID.  
Receiver keeps track of processed IDs.  
So, both sides must support de-duplication.  

💡 Example:  
If an app sends a confirmation email:  
Without de-duplication: The same email might be sent twice on retry.  
With de-duplication: The receiver sees the same ID and avoids resending.  

- It's hard to detect failures in distributed systems due to their complex nature—especially because networks are asynchronous, meaning delays or lost messages don’t clearly indicate success or failure.
- In distributed systems, the asynchronous network makes it hard to tell if a node has crashed or is just slow to respond, since delays and failures can look the same.
#### ⏱ Timeouts in Distributed Systems  
✅ Used to detect failures when nodes don’t respond in time.  
🌐 Asynchronous networks can delay messages indefinitely.  
⏳ Timeout sets an upper limit on how long to wait.  
❌ If response exceeds this limit, the node is assumed failed.  
⚖️ Trade-off:  
Short timeout → risk of false failure (node was just slow).  
Long timeout → slow system (waiting on crashed nodes).  

#### ⚖️ Trade-off for Small Timeout Value  
✅ Faster failure detection — system doesn’t wait long for crashed nodes.  
⛔ Higher risk of false failure — slow (but healthy) nodes may be wrongly marked as failed.  
📉 Can lead to unnecessary recovery actions or retries.  
![image](https://github.com/user-attachments/assets/6516c197-7079-4dfe-912c-0c82298a8487)  









