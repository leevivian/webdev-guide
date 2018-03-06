# Web Development Guide

## HTTP
Hypertext Transfer Protocol
* *Hypertext* is structured text that uses logical links (*hyperlinks*) between nodes containing text. 
* HTTP is the protocol to exchange or transfer hypertext
* Functions as a *request-response* protocol in the client-server computing model
* Is *stateless protocol*: does not require the HTTP server to retain information or status about each user

### How HTTP Works
* Client (ex. Web browser) submits an HTTP *request* to the server
* The server (ex. an application running on a computer hosting a website) provides resources like HTML files and other content, returns a *response*
	* The response contains completion status information about the request
### HTTP Request Methods
1. *GET*: requests a representation of the specific resource
	* Retrieves data
2. *HEAD*: Asks for a response identical to the GET request, without a response body
	* useful for retrieving meta-information written in response headers
3. *POST*: Request the server accept the entity enclosed in the request as a new subordinate of the web resource identified by the URI
	* ex. a *block of data* that is the result of submitting a web form
	* an item to add to a database
4. *PUT*: Requests the enclosed entity be stored under the supplied URI
	* If the URI refers to an already existing resource, it is modified
	* If the URI does not point to an existing resource, the server create the resource with that URI
5. *DELETE*: Deletes the specified resource

### HTTP Status Codes
1. *1xx Informational Responses*
	* Request was received and understood
	* Issued on Provisional basis while request processing continues, alerts client to wait for a final response
2. *2xx Success*
	* *200 OK:* Standard response for successful HTTP requests
		* from a GET, response contains entity corresponding to requested resource
		* From a POST, response contains entity desiring the result of the action
	* *201 Created:* Creation of new resource
	* 202 Accepted: Request has been accepted but processing is incomplete
	* *204 No Content:* Server successfully processed request but is not returning any content
3. *3xx Redirection*
	* Indicates client must take additional action to complete the request
	* Used in URL Redirection
4. *4xx Client Errors*
	* 400 Bad Request: Server cannot or will not process the request
		* Malformed request syntax, size too large, etc.
	* *401 Unauthorized*: Authentication is required and has failed or has not yet been provided
		* Response includes a WWW-Authenticate header
		* User does not have the necessary credentials
	* *403 Forbidden*: Request was valid, but the server is refusing action
		* User might not have permissions for a resources or may need an account
	* *404 Not Found*: The requested resource couldn’t be found
5. *5xx Server Error*
	* Server knows that is has encountered an error and cannot perform the request

# Web vs Application Server, N-tier Architecture
## Web Server
* Designed to serve HTTP content
* Serve static content, but can use plugins to support scripting languages and generate dynamic HTTP content
* Servers content to the web using http protocol
* Main job: Display site content
* /Example/: Apache Tomcat HTTP Server

## Application Server
* Can also server HTTP Content but is not limited to just HTTP
* Serve dynamic content
* Has Web Servers as integral part of them -> Can do whatever Web Servers are capable of
* Main job: hosts and exposes business logic and processes, the interaction between the user and displayed content
* Can support Application level services:
	* Connection Pooling
	* Object Pooling
	* Messaging Services
* /Example/: Oracle WebLogic

## N-tier Architecture
1. Front-end Web Server serving static content
2. Middle dynamic content processing and generation level application server (Symfony, Spring, Django, Rails)
3. Back-end database or data store - database management system software that manages and provides access to the data

## Client-side vs Server-side
* The two sides communicate via HTTP requests and responses
* Example: PHP is server-side code
	* They retrieve records from databases, maintain state, never have source code exposed to the user
* JavaScript is Client-side language, resides and runs on the browser
* PHP is executed on the server and outputs HTML, JavaScript which is sent as the response to the client
* The client is where the HTML is interpreted, and the JavaScript is executed

### Static vs Dynamic content
* *Static content*: HTML/CSS, images, javaScript
* Data is the same for each and every request
* Can be cached

* *Dynamic content*: are generated individually for each request by a server side program

# Internet Protocol Suite; TCP/IP
Foundational Protocols:
1. Transmission Control Protocol
2. Internet Protocol

The Suite: 
* Provides end-to-end communication specifying how data should be packetized, addressed, transmitted, routed, and received
1. *Link Layer:* (MAC) Contains communication methods for data that remains within a single network segment
	* Has the networking scope of the local network connection to which a host is attached
	* move packets between the Internet layer interfaces of two different hosts on the same link
	* *Packet*: Chunk of information, travels via routing
2. *Internet Layer:* (IP) Provides internet working between independent networks
	* Handles delivery of data
	* Sends packets across multiple networks, from the source network to the destination network
	* *IP* - Internet Protocol address, a numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication
	/Two purposes:/
		* Host/network interface identification
		* Packet *Routing*: Sending packets of data from source to destination by forwarding them to the next network router closer to the final destination
	IPv4 defines an IP address as a 32-bit number
	IPv6 uses 128 bits (ongoing)
3. *Transport Layer:* (TCP) Handling host-to-host communication
	* Connection-oriented protocol
	* WWW, email, file transfer rely on TCP
	* reliable stream delivery service which guarantees that 
		* all bytes received will be identical with bytes sent 
		* data arrives in the correct order
	* keeps track of units of data transmission that a message is divided into for efficient routing through the network. 
		* when an HTML file is sent from a web server, the TCP layer divides the sequence of file octets into segments and forwards them individually to the IP software layer (Internet Layer). 
		* The Internet Layer encapsulates each TCP segment into an IP packet by adding a header that includes (among other data) the destination IP address. 
		* When the client program on the destination computer receives them, the TCP layer (Transport Layer) re-assembles the individual segments and ensures they are correctly ordered and error-free as it streams them to an application.
4. *Application Layer:* Provide process-to-process data exchange for applications
	* Specifies the protocols used by most applications for providing user services or exchanging applications at a over the network connection
	Examples:
		* HTTP (HyperText Transfer Protocol)
		* FTP (File Transfer Protocol)
	* Treats transport layer and other lower protocols as ways to provides a stable network connection for communication

* Encapsulation is used to provide abstraction of protocols and services
* *Protocol* - absolute rule

* *Domain Name System* - a protocol for how computers exchange data on the Internet, known as *TCP/IP protocol suite*
	* turns a user-friendly domain name (reddit.com) into an IP address that computers use to identify each other on the network
	* Computer’s “GPS for the Internet”
	* Computers use an IP address to route your request to the site you’re trying to reach (like dialing a phone number)
	* Thanks to DNS, you don’t have to keep an address book of IP Addresses, you just connect through a domain name server, which manages a massive database that *maps domain names to IP addresses*

# Sockets
An internal endpoint for sending or receiving data at a single node in a computer network
* Client knows hostname + port number on which the server is listening, client needs to identify itself and bind to a local port that it will use during this connection (assigned by the system)
* Server accepts the connection, server gets a new socket bound to the same local port and has its remote endpoint set to the address and port of the client
	* It needs a new socket so that it can continue to listen to the original socket for connection requests while tending to the connected client
* Client-side: if the connection is accepted, a socket is successfully created and the client can use the socket to communicate with the server

