## Kafka Event Processing – Interview Questions and Answers

### 🟢 Beginner-Level

1. **What is Kafka and why is it used?**

   * Kafka is a distributed event streaming platform used for building real-time data pipelines and streaming applications. It enables high-throughput, low-latency transmission of messages between producers and consumers.

2. **What is a topic in Kafka?**

   * A topic is a category or feed name to which records are published. Producers send messages to topics, and consumers subscribe to topics to read messages.

3. **What’s the difference between a producer and a consumer in Kafka?**

   * A producer writes data to Kafka topics, while a consumer reads data from topics.

4. **What is a Kafka broker?**

   * A broker is a Kafka server that stores and serves messages. A Kafka cluster consists of multiple brokers.

5. **What is Zookeeper and why was it needed in Kafka?**

   * Zookeeper is used to manage Kafka cluster metadata, leader election, and configuration. Kafka is moving away from Zookeeper in newer versions.

6. **How does Kafka ensure message durability?**

   * Kafka writes messages to disk and replicates them across brokers. Acks and replication factors determine durability.

7. **What is the difference between Kafka and a traditional message queue (like RabbitMQ)?**

   * Kafka is designed for high-throughput distributed event streaming, retains messages longer, and uses a pull model for consumers. Traditional queues often use a push model and may not retain messages once consumed.

8. **Can a message be consumed by multiple consumers? Explain consumer groups.**

   * Yes, by assigning consumers to different groups. Each group gets its own copy of the message. Within a group, each partition is assigned to one consumer.

9. **How do you produce or consume messages in Kafka using Node.js (or Java, Python, etc.)?**

   * Use libraries like `kafkajs` (Node.js), `kafka-python`, or `confluent-kafka`. You connect to the Kafka broker, create a producer or consumer instance, and use `send` or `subscribe` methods.

10. **What happens if a consumer crashes after receiving a message but before processing it?**

    * If the consumer has not committed the offset, the message will be reprocessed after restart.

---

### 🟡 Intermediate-Level

11. **What are partitions in Kafka and why are they important?**

    * Partitions allow Kafka to parallelize data processing and scale horizontally. Each partition is an ordered, immutable sequence of records.

12. **How does Kafka ensure message ordering?**

    * Kafka guarantees order only within a partition. Ordering across partitions is not guaranteed.

13. **How is offset managed in Kafka?**

    * Offsets are stored per consumer group per partition and can be managed automatically or manually.

14. **What is the purpose of Kafka retention policies?**

    * To control how long messages are retained in a topic regardless of whether they have been consumed.

15. **What are the different delivery semantics in Kafka?**

    * At most once: Messages may be lost but never redelivered.
    * At least once: Messages are never lost but may be redelivered.
    * Exactly once: Messages are neither lost nor redelivered (requires extra config).

16. **How would you implement dead-letter queues in Kafka?**

    * Use a separate topic to store failed messages. If a message processing fails after retries, send it to the DLQ topic.

17. **What is idempotency in Kafka producer, and why is it useful?**

    * Ensures that duplicate messages are not written to Kafka even if retries occur. Prevents duplication during transient failures.

18. **Explain how backpressure is handled in Kafka consumers.**

    * Kafka uses a pull model, so consumers control their read rate. If they slow down, they simply lag behind.

19. **How does Kafka handle high throughput and scalability?**

    * Kafka partitions topics, distributes them across brokers, and uses efficient I/O and batching for high performance.

20. **What are Kafka Connect and Kafka Streams?**

    * Kafka Connect: Tool for ingesting/exporting data between Kafka and external systems.
    * Kafka Streams: A Java library for building stream processing applications on top of Kafka.

---

### 🔴 Advanced-Level

21. **How would you implement real-time processing with Kafka and external systems?**

    * Use Kafka Streams or a stream processor (e.g., Flink, Spark Streaming) to consume, process, and write results back to Kafka or other systems.

22. **What are common strategies for schema evolution in Kafka messages?**

    * Use Avro/Protobuf with Confluent Schema Registry. Ensure compatibility (backward/forward) in changes.

23. **What is log compaction, and how is it different from log retention?**

    * Log compaction keeps the latest message per key, useful for snapshots. Retention keeps all messages for a time or size.

24. **How do you monitor Kafka performance and lag?**

    * Use metrics exposed by Kafka + tools like Prometheus, Grafana, Burrow, Confluent Control Center.

25. **What are ISR (In-Sync Replicas) and how do they affect reliability?**

    * ISR are replicas that are fully caught up with the leader. Kafka only commits messages when written to all ISR.

26. **What’s the role of exactly-once semantics (EOS) in event processing?**

    * Ensures messages are processed once and only once. Requires idempotent producers and transactional writes.

27. **How would you secure a Kafka cluster?**

    * Use SSL/TLS encryption, SASL for authentication, and ACLs for authorization.

28. **How would you design a Kafka-based system to handle millions of events per minute?**

    * Use multiple partitions, scale consumers horizontally, enable compression, batch messages, and tune configurations.

29. **How would you handle data reprocessing and replay in Kafka?**

    * Reset consumer offsets, use compacted/retained topics, or design topics to allow replayability.

30. **How would you build a custom consumer for GitHub events using Kafka?**

    * Create a GitHub webhook → push events to Kafka topic → create Kafka consumer (Node.js or Python) → process events for CI/auditing/etc.
