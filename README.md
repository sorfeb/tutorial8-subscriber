## 1. what is amqp?
> AMQP stands for Advanced Message Queuing Protocol. It's an open-standard application layer protocol for message-oriented middleware, designed for reliable, efficient communication between applications for queuing messages between different components.

## 2. what it means? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is localhost:5672 is for? 
> **guest:guest@localhost:5672** is the connection string for accessing an AMQP broker. guest:guest are the username and password for accessing the broker. In this case, both are set to 'guest'. @localhost:5672 specifies the hostname and port of the AMQP broker. localhost refers to the local machine (where the code is running), and 5672 is the default port for AMQP. So, the code is trying to connect to an AMQP broker running on the local machine.

## Simulation slow subscriber
![image](https://github.com/sorfeb/tutorial8-subscriber/assets/112263712/38edf448-df23-4eb5-9d07-522f914ebe7e)
The `Queued messages` chart shows that the number of queued messages is 15 after I activated a 1 second delay for each process in the `subscriber` `main.rs` source code and triggered `cargo run` 3 times in a row. The number of queued messages from the publisher will be queued as long as the prior messages haven't been processed completely by the subscriber. 

## Reflection and Running at least three subscribers
![image](https://github.com/sorfeb/tutorial8-subscriber/assets/112263712/0165faab-1f3a-4616-a23f-0c23a592b3f0)
![image](https://github.com/sorfeb/tutorial8-subscriber/assets/112263712/5cdc499c-6b79-438c-beb9-13bd4c928151)
As you can see the messages from the `publisher` are automatically processed by the three instances of `subscribers`, resulting each subscriber split the processing workload everytime publisher pushes the 5 messages. This caused the performance to improve evident in the RabbitMQ charts showing no queued messages although the message rate increased.
