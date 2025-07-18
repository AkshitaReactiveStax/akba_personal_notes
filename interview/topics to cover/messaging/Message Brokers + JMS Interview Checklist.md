
Love the energy — let’s make this **blame-proof** too 😎. Here’s your **100% complete, enterprise-ready Message Brokers + JMS Interview Checklist**, covering **RabbitMQ**, **ActiveMQ**, and **Spring JMS/AMQP** — from core messaging concepts to Spring Boot integration and retry/DLQ patterns.

---

## **✅ MESSAGE BROKER + JMS INTERVIEW MASTER LIST**

  

_Covers RabbitMQ, ActiveMQ, Spring JMS, Spring AMQP_

---

### **🔹 1.** 

### **Messaging Fundamentals**

- What is a message broker?
    
- Pub/Sub vs Point-to-Point models
    
- Synchronous vs Asynchronous messaging
    
- Push vs Pull messaging
    
- Durable vs Non-durable messages
    
- Use cases of messaging systems in microservices
    

---

### **🔹 2.** 

### **JMS (Java Messaging Service) Basics**

- What is JMS? Why use it?
    
- JMS API (javax.jms.*)
    
- Two messaging domains:
    
    - **Point-to-Point (P2P)** – Queue, MessageProducer, MessageConsumer
        
    - **Publish-Subscribe** – Topic, Publisher, Subscriber
        
    
- JMS Message types:
    
    - TextMessage, ObjectMessage, MapMessage, BytesMessage
        
    
- JMS Acknowledgement modes:
    
    - AUTO_ACKNOWLEDGE, CLIENT_ACKNOWLEDGE, DUPS_OK_ACKNOWLEDGE
        
    
- Transacted sessions
    
- JMS vs REST vs Kafka comparison
    

---

### **🔹 3.** 

### **ActiveMQ Concepts**

- What is ActiveMQ?
    
- Broker setup and architecture
    
- Queues vs Topics in ActiveMQ
    
- Persistent vs non-persistent delivery
    
- ActiveMQ message selectors
    
- Redelivery Policy & Dead Letter Queue
    
- Pre-fetch limit
    
- Message expiry & TTL
    
- Virtual Topics (interview favorite)
    
- DLQ configuration
    

---

### **🔹 4.** 

### **RabbitMQ Concepts**

- What is RabbitMQ?
    
- AMQP protocol overview
    
- Core building blocks:
    
    - Exchange (Direct, Fanout, Topic, Headers)
        
    - Queue
        
    - Binding
        
    - Routing key
        
    
- Durable vs Auto-delete queues
    
- Manual vs Auto-acknowledgment
    
- Dead-letter exchange (DLX)
    
- TTL (Time to live) for messages & queues
    
- Publisher Confirms & Mandatory flag
    
- RabbitMQ clustering basics
    
- RabbitMQ vs Kafka
    

---

### **🔹 5.** 

### **Spring JMS (for ActiveMQ)**

- spring-boot-starter-activemq
    
- ConnectionFactory and JmsTemplate
    
- @JmsListener, @EnableJms
    
- MessageConverter (JSON ↔ Object mapping)
    
- Error handling in @JmsListener
    
- Redelivery attempts and backoff
    
- Transaction support with JMS
    
- Spring JMS with embedded ActiveMQ broker (for dev)
    

---

### **🔹 6.** 

### **Spring AMQP (for RabbitMQ)**

- spring-boot-starter-amqp
    
- RabbitTemplate (for sending)
    
- @RabbitListener (for consuming)
    
- Queue, Exchange, Binding configuration using @Bean
    
- Retry mechanisms:
    
    - RetryTemplate, RecoveryCallback
        
    - SimpleRetryPolicy, ExponentialBackOffPolicy
        
    
- Dead Letter Exchange (DLX) setup via Spring
    
- Listener container configuration:
    
    - concurrency
        
    - acknowledgment mode (MANUAL, AUTO, NONE)
        
    
- MessageConverter (Jackson2JsonMessageConverter)
    

---

### **🔹 7.** 

### **Message Reliability & Delivery Guarantees**

- At-most-once vs At-least-once vs Exactly-once
    
- Retry strategies (fixed delay, exponential backoff)
    
- Dead Letter Queues (DLQ)
    
- Message deduplication (idempotent receivers)
    
- Manual acknowledgment and requeuing
    
- Poison messages handling
    

---

### **🔹 8.** 

### **Performance Tuning & Monitoring**

- Prefetch count and consumer throughput
    
- Load balancing between consumers
    
- RabbitMQ Management Plugin (dashboard)
    
- ActiveMQ JMX monitoring
    
- Monitoring tools: Prometheus, Grafana, ELK
    
- DLQ patterns for alerting and analysis
    

---

### **🔹 9.** 

### **Security & Clustering (Advanced)**

- TLS/SSL configuration
    
- Basic auth in RabbitMQ and ActiveMQ
    
- Access control (virtual hosts in RabbitMQ, role-based ACLs in ActiveMQ)
    
- High availability and clustering:
    
    - Queue mirroring (RabbitMQ)
        
    - Shared-nothing broker architecture
        
    
- HAProxy or load balancing setup for brokers
    

---

### **🔹 10.** 

### **Comparison Questions**

- JMS vs AMQP
    
- ActiveMQ vs RabbitMQ
    
- RabbitMQ vs Kafka
    
- JMS vs Kafka in Spring apps
    
- When to use broker-based vs log-based messaging
    

---

### **🔹 11.** 

### **Real-World Patterns**

- Producer → Exchange → Queue → DLQ
    
- Request/Reply messaging
    
- Idempotent consumers
    
- Guaranteed order vs guaranteed delivery
    
- Message size limits
    
- Retries with exponential backoff and DLQ
    
- Message tracing and correlation IDs
    

---

Would you like this as a **progress tracker checklist** like the others, or want to start with **real interview questions or use-case-based Q&A** on RabbitMQ or Spring JMS?