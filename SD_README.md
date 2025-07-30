# System Design  
Concepts aims to build systems that are reliable, effective, and maintainable.  

- System design borrows many great concepts from **distributed systems**. Apart from distributed systems, some basic concepts on **computer networking** and **operating systems** are also helpful before taking this course.  

## Distributed system  
- A distributed system is a system whose components are located on different networked computers, which communicate and coordinate their actions by passing messages to one another.  
<img src="https://github.com/user-attachments/assets/88b0b155-2a48-41ec-9956-95f33c734608" alt="image" width="85%" height=" ">  

- Performance is the degree to which a software system or component meets its objectives for timeliness.  
- Scalability is the capability of a system, network, or process to handle a growing amount of work, or its potential to be enlarged to accommodate that growth.  
  - If we build a distributed system, we can split and store the data in multiple computers, and distribute the processing work.  
    - Vertical scaling refers to the approach of scaling a system by adding resources (memory, CPU, disk, etc.) to a single node. Meanwhile, horizontal scaling refers to the approach of scaling by adding more nodes to the system.  
- Availability is the probability of a system to work as required, when required, during a mission.  
- Redundancy is one of the widely used mechanisms to achieve higher availability. It refers to storing data into multiple, redundant computers. So, when one computer fails, we can efficiently switch to another one. This way, we’ll prevent our customers from experiencing this failure.  

- To help Developers build better systems, Scientists created a collection of false assumptions.  
<img src="https://github.com/user-attachments/assets/67e62a6c-2456-471d-b360-a15f9e6b664f" alt="image" width="85%" height=" ">

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
<img src="https://github.com/user-attachments/assets/b661698f-daa8-42b8-a104-bec9fe104ee7" alt="image" width="75%" height=" ">   

- In **Fail-Stop** - node remain halted permanantely and other node detects it.  
- In **Crash** A node halts, but silently. So, other nodes may not be able to detect this state. It can only identify when they communicate with it.  
- In **Omission** A node fails to respond to incoming requests.  
- **Byzantine failures** occur when a node does not behave according to its specific protocol or algorithm. This usually happens when a malicious actor or a software bug compromises the node.  

### Exactly-Once Semantics  
- Multiple deliveries of a message: There might be a case for sending multiple messages due to network issue, but it could be a problem when it comes to bank trasfers, one bank may charge twice.  
   - To avoid such situation we have to use approach where the node process the message only one time. though it may be delivered multiple times.  
   - We can use Idempotent Operation- No matter how many times you perform the operation (once or 100 times), the end result is exactly the same as if it were performed once.  
      - RESTful design treats a PUT request as idempotent.    
<img src="https://github.com/user-attachments/assets/6dc368bb-a776-40dc-a143-8c55d7dbd1d7" alt="image" width="75%" height=" ">  
<img src="https://github.com/user-attachments/assets/762548da-4e1f-4cd9-a4f9-760677574414" alt="image" width="75%" height=" ">  
<img src="https://github.com/user-attachments/assets/f63f7da1-62b4-4e1a-83e2-e614a369e206" alt="image" width="75%" height=" ">  

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
<img src="https://github.com/user-attachments/assets/6516c197-7079-4dfe-912c-0c82298a8487" alt="image" width="85%" height=" ">  
- A failure detector is the component of a node that we can use to identify other nodes that have failed.

#### ⚙️ Properties of Failure Detectors (Concise)  
- Completeness: How well the detector finds actual crashed nodes.  
- Accuracy: How often it avoids false alarms (wrongly declaring a node as failed).  

✅ Perfect Failure Detector  
- Detects all real failures (complete).  
- Makes no mistakes (accurate).  
❌ Not possible in fully asynchronous systems.  

#### Stateless System.  
- Doesn’t remember past requests  
- Works only with current input  
- No stored data between calls  
Example:
A price calculator service that gets product price and discount from other services every time — it doesn’t store anything.  
#### Stateful System  
- Remembers past interactions  
- Keeps data like session info or user activity  
- Future behavior may depend on past input    
<img src="https://github.com/user-attachments/assets/b82168f7-bc07-4db2-8e3e-76b8e66cb455" alt="image" width="85%" height="">  

#### Stateful System  
- Remembers past data  
- Stores and updates internal state  
- Output depends on current state + input  
Example:
A system that stores employee ages and returns the maximum age — result depends on what’s already stored.  
<img src="https://github.com/user-attachments/assets/3bab833a-d9c8-4930-ba59-42fd397344d8" alt="image" width="50%" height=" ">

##### ✨ Interesting Observations  
✅ Stateful systems are powerful because computers can store and process large amounts of data better than humans.  
⚙️ Maintaining state adds complexity: deciding storage, processing, backups, syncing, etc.  
🏗️ Best practice:  
Keep stateless components for business logic.  
Use stateful components separately for data storage.  

📈 Benefits of Stateless Systems Over Stateful Systems  
✅ Easier to design, build, and scale.  
🔄 All servers are identical, so traffic can be balanced easily.  
🚀 Scaling (adding/removing servers) is simple.  
But:  
❌ Stateful systems are harder:  
Different servers store different data.   
Extra work needed for syncing and routing correctly.  

##### 🚀 Scalability  
Scalability means the ability to handle larger datasets and workloads by adding more resources (like servers or CPUs).  
It helps go beyond the limits of a single machine.  
⚙️ How to Achieve Scalability:  
A main technique is partitioning — splitting data or tasks into smaller pieces that can be processed in parallel across multiple systems.  
##### There are two different variations of partitioning:  
Vertical partitioning & Horizontal partitioning (or sharding)  
<img src="https://github.com/user-attachments/assets/b27db598-adce-4cc3-bc07-0adf764c16a4" alt="image" width="70%" height=" ">  

**🧩 What is a Node?**  
A node is a single computer or server in a network or distributed system.  
In a database cluster (e.g., MongoDB, Cassandra), each node stores part of the data.  
Nodes communicate with each other to answer queries and perform operations.  
Example: Netflix might store user profiles on Node A, and watch history on Node B.  

**🔹 Vertical Partitioning**  
What it is: Splitting a table by columns into smaller tables.  
Why: To store related columns separately and reduce data size per table.  
How: Use joins to link tables back together.  
Example: One table stores Name, Age, another stores Address, Phone.  
Note: This is similar to normalization, but vertical partitioning can go beyond that, even on already normalized data.  

Limitation: Joins across tables (and nodes) become slower.

**🔹 Horizontal Partitioning (Sharding)**  
What it is: Splitting a table by rows into smaller subsets.  
Why: To spread data across multiple machines for scalability.  
How: Split rows using criteria like student surname A–M and N–Z.  
Benefit: Each node handles only part of the data, improving performance and scalability.  
Limitation:  
Hard to maintain transactions across nodes.  
Range queries may still need multiple nodes.  
⚠️ Trade-offs in Partitioning  
Vertical partitioning: Easier joins locally but complex in distributed systems.  
Horizontal partitioning: Scales better, but transactions and range queries across nodes are harder.  
No perfect solution — we must choose based on system needs. 

**Conclusion**  
Vertical partitioning is a data modeling technique done by engineers, often independent of the storage system. Horizontal partitioning, on the other hand, is a core feature of distributed databases and requires engineers to understand the system's internal workings. Hence, the focus is usually on horizontal partitioning.  
🧮 What is Normalization?  
Normalization is the process of organizing a database to reduce data redundancy and improve data integrity.  
Involves breaking a big table into smaller related tables.  
Uses foreign keys to connect them.  

**⚙️ What is Sharding (Horizontal Partitioning)?**  
Sharding is a database architecture pattern where data is split by rows across multiple servers (nodes).   
Used for scalability and faster access in large systems.  
Each shard (node) holds part of the data.  
✅ Example:    
Netflix stores users whose names start with A-M on Shard 1, and N-Z on Shard 2.  

#### Netflix and Uber (Horizontal + Vertical Partitioning) Sample  
<img src="https://github.com/user-attachments/assets/d34ca718-f97e-49d9-9fc2-7dcded7c13af" alt="image" width="70%" height=" ">  

🔹 What is a Shard?  
A shard is a subset of data from a large dataset—split horizontally by rows—and stored separately for performance and scalability.  

🔹 What is a Node?  
A node is a physical or virtual machine/server (or a database instance) that stores and processes a shard.  
✅ So: A shard is data, and a node is hardware/software that holds that data.  

<img src="https://github.com/user-attachments/assets/80f3548b-e94a-45b0-93c5-8aaef1a1dc98" alt="image" width="70%" height=" ">  

<img src="https://github.com/user-attachments/assets/a6f826ca-db8e-46eb-a412-63c643d8b00c" alt="image" width="70%" height=" ">    

<img src="https://github.com/user-attachments/assets/ea1914ca-7725-4f26-82e0-0485efb847ef" alt="image" width="70%" height=" ">     

<img src="https://github.com/user-attachments/assets/f70f465d-1210-40fa-8429-a0b4bc8dea5b" alt="image" width="70%" height=" ">  

----------------------------------------------------------------------------------------------------------------------------  
#### System in reality improve over iterations. We often start with something simple and when the bottleneck arises one or other new design become necessary.  

**** Recommended is 2 iteration at first to start with.  
- Software Developer must know system design- once data is passed from front end handelling data at back end is crucial.
- System Design may have multiple possible soultions.
- You may be give real time application buidling like whats aap, which has many features but in interview the time is less so we can produce some core functionality according to interviewer question.
- Best Pactcice = Solidify the requirement --> Scope the problem --> Engage the Interviewer.
- Responsibility of Designer : we need to provide fault tolerance at design level because modern systems use shelf components and have millios of such component if something is breaking down, we need to hide the undesirable reality from the customer.
### FUndamental concepts in system design interview.  
#### a) PACELC Theorem  

















