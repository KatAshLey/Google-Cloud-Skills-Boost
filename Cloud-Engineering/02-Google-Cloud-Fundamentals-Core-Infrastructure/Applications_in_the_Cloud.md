<h1>Applications in the Cloud</h1>
<h2>Cloud Run</h2>

* A managed compute platform tha can run stateless containers
* Serverless, removing the need for infrastructure management
* Built on Knative, an open API and runtime environment built on kubernetes
* Automatically scale up and down from zero almost instantaneously, charging only for resources used
* Handles HTTP serving

**Developer workflow**
* Write your code/source code
* Build and package container image
* Deploy to Cloud Run, web app

**Container based** workflow has a great a mount of transparency and flexibility. Concentrating on application rather than infrastructure.

**Source based workflow**
* Write your code/source code
* Deploy to CLoud Run, which builds the source and packages the application into a container using Buildpacks(open source project)

**Costs** you only pay for startup, shut down, when its handling requests and a small fee for every million of requests you run. Price increases with CPU and memory.

**Binary linux 64bit** can run on Cloud Run, meaning it can run popular programming languages such as Java, Python, node.js, PHP, Go and C++. it can also run Cobol, Haskell and Perl, as long as your application can handle web requests.

<h2>Development in the Cloud</h2>

**Cloud Run Functions** write a single purpose function that completes  steps and arranges for it to automatically run whenever the event is triggered.

* Lightweight, event-based, asynchronous compute solution
* Can create small, single-purpose functions tha respond to cloud events without the need to manage a server or a runtime environment
* Construct application workflows from individual business logic tasks and connect and extend cloud services
* Billed to the nearest 100 milliseconds while your code is running
* Supports writing source code in a number of programming languages including Node.js, Python, Go, Java, .Net Core, Ruby and PHP

Events from Cloud Storage and Pub/Sun can trigger Cloud Run functions asynchronously or you can use HTTP invocation for synchronous execution.

