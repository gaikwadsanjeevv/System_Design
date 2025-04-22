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


