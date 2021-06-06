# Enterprise-Service-Bus

I do not want to start a debate on wether XI is an ESB, but more of a statement to what is SAP ESB (if XI it is, then be it).

We also discuss uses of SAP ESB in production currently and what kind of environment (i.e. strictly SAP backend systems, or combination of various vendors backend systems).

## What is an ESB? 

As a reminder, an ESB is expected to exhibit the following characteristics (source Wikipedia):

• It is usually operating-system and programming-language agnostic; for example, it should enable interoperability between Java and .NET applications.

• It uses XML (eXtensible Markup Language) as the standard communication language.

• It supports web-services standards.

• It supports various MEPs (Message Exchange Patterns) (e.g., synchronous request/response, asynchronous request/response, send-and-forget, publish/subscribe).

• It includes adapters for supporting integration with legacy systems, possibly based on standards such as JCA

• It includes a standardized security model to authorize, authenticate and audit use of the ESB.

• To facilitate the transformation of data formats and values, it includes transformation services (often via XSLT or XQuery) between the format of the sending application and the receiving application.

• It includes validation against schemas for sending and receiving messages.

• It can uniformly apply business rules, enriching messages from other sources, the splitting and combining of multiple messages and the handling of exceptions.

• It can provide a unified abstraction across multiple layers

• It can route or transform messages conditionally, based on a non-centralized policy (i.e. no central rules-engine needs to be present).

• It is monitored for various SLA (Service Level Agreement) threshold message latencies and other SLA characteristics.

• It (often) facilitates "service classes," responding appropriately to higher and lower priority users.

• It supports queuing, holding messages if applications are temporarily unavailable.

## Successfull ESB Implementation

• Any successful implementation of SOA/ESA requires applications and infrastructure to support it's principles. This means all the applications either should have the ability to expose their functionality as services or they need an infrastructure to expose the service. SAP XI would definetly help to expose the application functionality as services(web). I dare to call as a 'service container' in ESB terminology.

• Besides the service repository functionality, XI also provides value added services like intelligent routing, mapping, auditing functionality etc.

• And also distributed deployment(ESB quality for scaling) of some of the XI components are possible. Say for example, adapter deployment options(central, decentral), PCK, proxy framework etc.

• On the security aspect of these exposed service, my understanding is that XI do not have much (like ws-security, xml signature, encryption, etc).

• Business Process Modelling(BPEL4WS conformance) can be used for the service choreography. *I am not sure whether CAF and VC supports BPEL standards.*

• *Can anybody throw some thougths on this?* And also what are the webservice management tools(deploying, declarative security etc) available in NetWeaver?

## Piecing together ESB + SOA Mechanism

I had quite a difficult time understanding the concept of ESB and how it fits into the SOA picture.

Reading across a lot of documents and trying out with a few ESB products have helped me to increase my understanding at least by a few notches.

Tis time taking experience motivated to put down my understanding in a blog. Hope will help to streamline the approach for people who are new to ESB.

## Blog Post 1- ESB Fundamentals, capabilities, components, mediation and usage patterns.

In this blog series, I will discuss about the following topics —

•Fundamentals of ESB

ESB -Capabilities

Components of an ESB

ESB –Mediation Patterns

ESB –Usage Patterns

Design Decisions

ESB –Deployment Models

In the first blog lets look into the fundamentals – need and definition of ESB and some basic concepts .

**Need for ESB**

The traditional architecture of point to point interfaces lead to high integration costs and inflexibility into the IT landscape. It has lead to the evolution of SOA architecture. ESB helps us to sustain SOA. It also helps us to enrich our Service Provisioning Capabilities.

**ESB Definition**

An enterprise service bus (ESB) is a software architecture for middleware that provides fundamental services for more complex architectures.
The ESB represents the piece of software that lies between the business applications and enables communication among them.

The diagram above shows the high level functions of the ESB.ESB should should be treated as a Software ans not as a hardware. Because of the name Service Bus it is sometimes confused as being a part of the hardware. But the term “Service Bus” is analogous. Use of the word “bus” stems from the physical bus that carries bits between devices in a computer. The enterprise service bus serves an analogous function at a higher level of abstraction. The inner bubbles such as Routing , Security consists of some of the functionality of ESB. We will discuss these in the sections below.

A more comprehensive definition would be –

In order to fully exploit the interoperability that Web Services provide, there is a need for a communications “architecture” which enables software applications that run

on different platforms and devices

written in different programming languages

use different programming models

require different data representations

ESB is positioned typically as a “middle ware‟ application, where it acts as a buffer layer for services exposed across a heterogeneous applications

An ESB provides

provides a standards-based integration platform

combines messaging, web services, protocol & data transformation, and intelligent routing

enables a highly distributed, loosely coupled event driven SOA in a heterogeneous environment

scales to support global deployment, and

provides the ability to be managed and monitored from a central point

Some Fundamental Concepts

The definitions and illustration of these fundamental concepts will help to understand Esb in a more conceptual way.

Point to Point v/s Mediated Central Communication

In point to point communication any two systems to interact with via a dedicated connection. With the increase in systems the number of dedicated connections increase beyond comfort. There are issues of maintenance and governance in such a landscape

In a Central landscape all messages and data flow through a central system – a Broker , an ESB or a Gateway. It helps to imply Central Governance , Security etc. The most important advantage is we do not need point to point connectors but only a connection from the concerned system to the ESB.

If we observe the above diagram, one realizes that in the point to point scenario when one designs an interface fro toe of the systems ; one has to understand the two systems in detail. Also for designing the interface for any two other systems ,again we have to understand the two system in detail.

ESB is positioned typically as a “middle ware‟ application, where it acts as a buffer layer for services exposed across a heterogeneous applications

An ESB provides

it provide s us advanced tools to map data structures and controls from one system to the other

it provides a standard abstraction; using the same skill set we can map different systems

it provides us tools to implement security , governance ,monitoring

it provides us options to manifest changes in the landscape with the help of configurations

 2. Mapping

” mce_src=”image

The diagram above gives an example of how an XML message was mapped via ESB into a new XML message. This is a typical instance of data structure inter- conversion for communication between systems.

We can have other manipulations on data like -data format conversion , Unicode- non Unicode conversions , data enrichment, data unification from two or more sources and so on.


3. Routing

Routing is the concept of sending input message to the required receiver ,In the about we have a diagram of a broadcast , where whole of the input message is being transmitted to all three receivers.

But we can have various types of routing based on our requirements –

1.Static Routing – by looking up service endpoint in ESB Name space Directory or Routing information table in database where the Itinerary defining which endpoint to visit is mentioned in the message

2.Dynamic Routing – Routing based on examining message content and configuration rules

3.Intelligent routing – Routing based on infrastructure intelligence (availability, workload) or detection of error situations

4.Itinerary Based routing – Message contains itinerary and process state. Message routed to next system based on itinerary.

5. Content Based Routing – In this input message is inspected and based on the routing rules, the routing is performed.

One practical example of routing could be –

We have raised a Sales Order Request , based on the Product Ordered– Corresponding Supplier relationship (which has been maintained in the routing table) , the ESB will invoke the Create Order Service in the corresponding Supplier’s System
