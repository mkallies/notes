# Messaging

As your application grows, you will have more and more services which will need to talk to each other. You can either talk to other services synchronously or asynchronously.

Synchronous between services can be problematic if there are sudden spikes of traffic

Asynchronous models with AWS
- SQS: queue model
- SNS: pub/sub model
- Kinesis: real-time streaming model

## SQS

Producer -> send message -> SQS queue <-> poll for messages -> Consumer

Standard queue
- Oldest offering
- Fully managed
- Scales from 1 message per second to 10,000s per second
- Default retention of messages: 4 days, max of 14 days
- No limit to how many messages can be in the queue
- Horizontal scaling via increasing consumers
- Can have duplicate messages
- Can have out of order messages (best effor ordering)
- Limitation of 256kb per message sent

Delay queue
- Delay a message up to 15 minutes
- Default 0 seconds
- Can set a default at queue level
- Can override the default using the DelaySeconds parameter

Producing Messages
- Define body (up to 256kb, string)
- Add message attributes (metadata - optional)
- Provide Delay Delivery (optional)

Consuming Messages
- Poll SQS for messages (receive up to 10 messages at a time)
- Process the message within the visibility timeout
- Delete the message using the message ID & receipt handle

Visibility timeout
- When a consumer polls a message from a queue, the message is "invisible" to other consumers for a defined period (Visibility Timeout)
  - Set between 0 seconds and 12 hours (default 30 seconds)
  - If too high (15mins) and consumer fails to process the message, you must wait a long time before processing the message again
  - If too low (30 sec) and consumer needs time to process the message (2 mins), another consumer will receive the message and the message wil be processed more than once
- ChangeMessageVisibility API to change the visibility while processing the message
- DeleteMessage API to tell SQS the message was successfully processed

Dead Letter Queue (DLQ)
- If a consumer fails to process a message within the Visibility Timoue the message goes back to the queue
- We can set a threshold of how many times a message can go back (redrive policy)
- After threshold has exceeded, the message goes into a DLQ
- Need to create a DLQ first then designate it dead letter queue
- Make sure to process the messages in the DLQ before they expire

Long Polling
- When a consumer request message from the queue, it can optionally wait for messages to arrive if there are none in the queue
- LongPolling decreases the number of API calls made to SQS while increasing the efficiency and latency of your service
- The wait time can be between 1 sec to 20 sec (20 sec is preferable)
- Prefer Long Polling over Short Polling
- Long polling can be enabled at the queue level or at the API level using WaitTimeSeconds 
