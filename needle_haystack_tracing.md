# How you too can find a needle in the haystack
Shreya Sharma, Expedia Inc.

Technical Product Manager

## The problem

[ sad face graphic ]

### Microservices Architecture
Made life really easy by taking the whole chucnk of architecture, and divided it into managable chunks.

But it also came with a lot of cons.

Such as: finding the root cause of an issue. Like "finding a needle in a haystack."

## So, how do we fix this?

[ considering graphic ]

### Google - Dapper Paper

Passing three IDs throughout the events. Those would be used to identify. 
1. Trace ID (transaction id, etc.). This helps you identify each transaction individually
2. Span ID. There are multiple spans within a transaction. Each service is uniqely defined by a span id.
3. Parent Span ID. Who talks to whom? 

So, what happened with this?

It became distributed tracing! 

[ happy face graphic ]

## Zipkin

Expedia ran a POC of zipkin. Loved it. 
Expedia built their own concept, called Haystack. 

Along with Haystack are things like X-Ray, Jaeger, etc. 

## Final Take-away

Go home, try out distributed tracing solutions (haystack, jager, x-ray). Get your hands dirty. Learn! 

# The Haystack is not getting any smaller