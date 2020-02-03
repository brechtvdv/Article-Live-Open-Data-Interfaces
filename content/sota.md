## Related work
{:#related_work}

### Web publication protocols

**HTTP polling** A client sends an HTTP GET request to the server, waits for a certain time interval after retrieving the response and starts again with requesting the resource. The benefit of this approach is that a resource becomes stateless and HTTP caching is possible. However, there is no strict guideline on how clients should time their request. For variantly updating resources, a client can’t predict when the next update will be available. A higher polling frequency can minimize the latency on the client, but this comes at a higher bandwidth cost[](cite:cites lubbers2016html5).

**HTTP long polling** With long polling, the server only returns a response when a new update is available. This way, a client does not send redundant requests like HTTP polling. Also, the client doesn’t wait before sending a request again. A resource becomes stateful as the server needs to maintain all the connections open. [](cite:cites 6197172) showed that long polling can have a similar performance as Websockets when the underlying network latency is lower than half the data measurement rate.

**Server-Sent Events** With the growing demand for (near) realtime applications, HTTP is extended in 2014 with the support of Server-Sent Events (SSE). Similarly to long polling, the server holds the connection open for every client, but this remains open for pushing multiple updates instead of one. With the use of the EventSource API (supported by all browsers except IE and Edge), clients can receive updates of a resource in an event-driven fashion. Using SSE over HTTP/1.1 has the disadvantage that every requested resource requires a separate TCP connection, which can run into the limited number of connections a browser can open per domain. However, this is solved for servers that support HTTP/2, which multiplex all requests and responses over one connection.

**Websockets** The Websocket protocol provides a bidirectional communication channel over one TCP connection for every client. HTTP is used to set up a handshake between client and server for transmitting data, but further communication happens over a raw TCP connection. The WHATWG Websocket standard describes how messages can be pushed between client and server, but there are also sub protocols (MQTT[](cite:cites 8088251), CoAP…) for more advanced features, for example a publish/subscribe broker to receive or send updates of a specific resource. Websockets has a similar performance as SSE[](cite:cites slodziak2016performance), but a lower transmission latency when the server needs to send large messages above 7.5 kilobytes. Also, for client to server communication provides Websockets a lower transmission latency[](cite:cites slodziak2016performance) than using HTTP.

### RDF Streams

[](cite:cites arasu2006cql) defines a stream S as a (possibly infinite) bag (multiset) of elements〈s, τ〉where s is a tuple (the actual data without the timestamp of the element) belonging to the schema of S and τ ∈ T is the timestamp of the element. The Resource Description Framework (RDF) Stream Processing Community Group (RSP), which focuses on processing RDF-modelled data, has applied this definition for RDF streams[](cite:cites dell2014rsp) where an RDF stream S is a (potentially) unbounded sequence of timestamped RDF statements in non-decreasing time order. TripleWave[](cite:cites mauri2016triplewave) is a tool that transforms Web streams, which only  differs from an RDF stream by its data model[](cite:cites rojas2018preliminary), into RDF streams and republishes them with a polling and/or push-based (Websockets, MQTT) interface. These streams can be consumed by other RDF stream processors (RSP) for continuous query answering with SPARQL-based query models (C-SPARQL[](cite:cites barbieri2010c), CQLS [](cite:cites le2011native), TPF Query Streamer [](cite:cites taelman_eswc_2016)). [](cite:cites dell'aglio2017on) describes for the publication of an RDF stream that both push-based and polling interfaces can be supported; the consumer may choose what it prefers. Also, several requirements[](cite:cites dell2017stream) are defined for RSP query engines of which requirement 6 “timely fashion” acknowledges [](cite:cites dell'aglio2017on) that the timing of results depend on the application scenario and thus the requirements of the consumer of the data publication or query service. In the next section, we will look into how the timely fashion requirement is applied for live Open datasets.

 <!-- While RDF allows data publishers to describe knowledge in triple-based statements, it is important to notice that a non-RDF Web stream of a live dataset only really differs from an RDF stream by its data model [](cite:cites rojas2018preliminary) and thus, we will look into how RDF streams are currently published on the Web. -->