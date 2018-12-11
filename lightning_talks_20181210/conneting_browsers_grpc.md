# Connect from Browsers using gRPC-Web
Stanley Cheung @ Google

## What is gRPC?
gRPC Remote Procedure Calls

It is a high performance, open source, general purpose, standards-based, feature-rich RPC framework. 

g doesn't stand for google!!

## gRPC Speaks Your Language

[ almost every modern language listed here ]

## gRPC Basics

1. Import code into your app
2. Define .proto 
3. Generate stubs in your language
3. Talk gRPC with someone else! 

...can we do the same thing in browsers? 

## gRPC-Web

_Not so fast!_

The answer, right now, is no. 

- STandard WEB APIs don't expose HTTP wire-transport details
- Web clients prefers text data: security, json compatible encoding, streaming
- response trailers are not supported
- web-specific features: CORS, security(CSRF/CSP), etc.
- Firewall, corporate proxies, etc. 

## gRPC-Wen Spec
- Aux protocol providing a translation layer between browser requests and gRPC
- Currently, the spec is implemented in Envoy. More to come
- Over HTTP/*, as negotiated by browsers
- ... (missed notes)

Graphic showing that basically, server side uses envoy as person-in-the-middle, and client (browser) connects to Envoy

# gRPC-Web
- GA since Oct 18
- grpc.io
- Used internally at Google