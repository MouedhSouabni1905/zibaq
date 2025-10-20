**Tags:** [[Programming]]

- Scalability: Your app is scalable if it can handle a large amount of solicitation
- Performance: Performance is an issue if your app is slow for any one single user
- **Latency** refers to the amount of time it takes for a system to respond to a request. **Throughput** refers to the number of requests that a system can handle at the same time. Generally, you should aim for maximal throughput with acceptable latency.
- For example, a system processes information in 2 steps. This means that input goes through step 1 then step 2. The combinational way is to sequentially wait for each input element to finish both steps before adding a new element. The pipeline way is to add the new element when the original element has moved on to step 2. If we abstract away and think of the system as black box, we can see that using the second way reduces latency and increases throughput. compared to first way.
- Availability: refers to the ability of a system to provide its services to clients even in the presence of failures. This is often measured in terms of the percentage of time that the system is up and running, also known as its uptime.
- Consistency: refers to the property that all clients see the same data at the same time. This is important for maintaining the integrity of the data stored in the system.
- Partition tolerance: if a network partition happens the system continues functioning properly.
- A distributed system is any system whose state is split across 2 or more systems.
- ^ is called the CAP theorem, which states that a distributed system can only fulfill 2 of the three criteria at one time.