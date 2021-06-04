# Enterprise-Service-Bus

Everything we know about ESB and SAP'sHi fellow sdners gurus I have been reading threads about SAP SOA and ESB.

I do not want to start a debate on wether XI is an ESB, but more of a statement to what is SAP ESB (if XI it is, then be it).

1) What is SAP ESB (Enterprise Service Bus) today (I could not find a clear answer to is)?

2) Who uses this SAP ESB in production currently and what kind of environment (i.e. strictly SAP backend systems, or combination of various vendors backend systems)?

Can someone share some light on this topic?

As a reminder, an ESB is expected to exhibit the following characteristics (source Wikipedia):

 It is usually operating-system and programming-language agnostic; for example, it should enable interoperability between Java and .NET applications.

 It uses XML (eXtensible Markup Language) as the standard communication language.

 It supports web-services standards.

 It supports various MEPs (Message Exchange Patterns) (e.g., synchronous request/response, asynchronous request/response, send-and-forget, publish/subscribe).

 It includes adapters for supporting integration with legacy systems, possibly based on standards such as JCA

 It includes a standardized security model to authorize, authenticate and audit use of the ESB.

 To facilitate the transformation of data formats and values, it includes transformation services (often via XSLT or XQuery) between the format of the sending application and the receiving application.

 It includes validation against schemas for sending and receiving messages.

 It can uniformly apply business rules, enriching messages from other sources, the splitting and combining of multiple messages and the handling of exceptions.

 It can provide a unified abstraction across multiple layers

 It can route or transform messages conditionally, based on a non-centralized policy (i.e. no central rules-engine needs to be present).

 It is monitored for various SLA (Service Level Agreement) threshold message latencies and other SLA characteristics.

 It (often) facilitates "service classes," responding appropriately to higher and lower priority users.

 It supports queuing, holding messages if applications are temporarily unavailable.

-----

Any successful implementation of SOA/ESA requires applications and infrastructure to support it's principles. This means all the applications either should have the ability to expose their functionality as services or they need an infrastructure to expose the service. SAP XI would definetly help to expose the application functionality as services(web). I dare to call as a 'service container' in ESB terminology.

Besides the service repository functionality, XI also provides value added services like intelligent routing, mapping, auditing functionality etc.

And also distributed deployment(ESB quality for scaling) of some of the XI components are possible. Say for example, adapter deployment options(central, decentral), PCK, proxy framework etc.

On the security aspect of these exposed service, my understanding is that XI do not have much (like ws-security, xml signature, encryption, etc).

Business Process Modelling(BPEL4WS conformance) can be used for the service choreography. I am not sure whether CAF and VC supports BPEL standards.

Can anybody throw some thougths on this. And also what are the webservice management tools(deploying, declarative security etc) available in NetWeaver?

-----



