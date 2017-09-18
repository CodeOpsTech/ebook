# Serverless Architectures:Demystifying Serverless Computing

<br>

<p align = "center"><font size = "4"><i><b>Serverless architectures refer to applications that depend a lot on third party
services known as BaaS (Backend as a Service), or on custom code which
runs on FaaS (Function as a Service).</i></b></font></p>

<br>

In the 1990s, Neal Ford (now at ThoughtWorks) was
working in a small company that focused on a technology
called Clipper. By writing an object-oriented framework
based on Clipper, DOS applications were built using dBase.
With the expertise the firm had on Clipper, it ran a thriving
training and consulting business. Then, all of a sudden, this
Clipper-based business disappeared with the rise of Windows.
So Neal Ford and his team went scrambling to learn and adopt
new technologies. “Ignore the march of technology at your
peril,” is the lesson that one can learn from this experience.
Many of us live inside ‘technology bubbles’. It is easy to
get cozy and lose track of what is happening around us. All
of a sudden, when the bubble bursts, we are left scrambling
to find a new job or business. Hence, it is important to stay
relevant. In the 90s, that meant catching up with things like
graphical user interfaces (GUIs), client/server technologies
and later, the World Wide Web. Today, relevance is all about
being agile and leveraging the cloud, machine learning,
artificial intelligence, etc.

With this background, let’s delve into serverless
computing, which is an emerging field. In this article, readers
will learn how to employ the serverless approach in their
applications and discover key serverless technologies; we will end the discussion by looking at the limitations of the
serverless approach.

### Why serverless?

Most of us remember using server machines of one form or
another. We remember logging remotely to server machines
and working with them for hours. We had cute names for the
servers - Bailey, Daisy, Charlie, Ginger, and Teddy - treating
them well and taking care of them fondly. However, there
were many problems in using physical servers like these:
 Companies had to do capacity planning and predict their
future resource requirements.
 Purchasing servers meant high capital expenses (capex)
for companies.
 We had to follow lengthy procurement processes to
purchase new servers.
 We had to patch and maintain the servers ... and so on.
The cloud and virtualisation provided a level of flexibility
that we hadn’t known with physical servers. We didn’t have
to follow lengthy procurement processes, or worry about
who ‘owns the server’, or why only a particular team had
‘exclusive access to that powerful server’, etc. The task of
procuring physical machines became obsolete with the arrival of virtual machines (VMs) and the cloud. The architecture
we used also changed. For example, instead of scaling up
by adding more CPUs or memory to physical servers, we
started ‘scaling out’ by adding more machines as needed,
but, in the cloud. This model gave
us the flexibility of an opex-based
(operational expenses-based)
revenue model. If any of the VMs
went down, we got new VMs
spawned in minutes. In short, we
started treating servers as ‘cattle’
and not ‘pets’.

However, the cloud and
virtualisation came with their own
problems and still have many
limitations. We are still spending a
lot of time managing them — for
example, bringing VMs up and down, based on need. We have
to architect for availability and fault-tolerance, size workloads,
and manage capacity and utilisation. If we have dedicated VMs
provisioned in the cloud, we still have to pay for the reserved
resources (even if it’s just idle time). Hence, moving from a
capex model to an opex one is not enough. What we need is to
only pay for what we are using (and not more than that) and
‘pay as you go’. Serverless computing promises to address
exactly this problem.

The other key aspect is agility. Businesses today need
to be very agile. Technology complexity and infrastructure
operations cannot be used as an excuse for not delivering
value at scale. Ideally, much of the engineering effort should
be focused on providing functionality that delivers the
desired experience, and not in monitoring and managing the
infrastructure that supports the scale requirements. This is
where serverless shines.

### What is serverless?

Consider a chatbot for booking movie tickets - let’s call it
MovieBot. Any user can make queries about movies, book
tickets, or cancel them in a conversational style (e.g., “Is
‘Dunkirk’ playing in Urvashi Theatre in Bengaluru tonight?”
in voice or text).

This solution requires three elements: a chat interface
channel (like Skype or Facebook Messenger), a natural
language processor (NLP) to understand the user’s intentions
(e.g., ‘book a ticket’, ‘ticket availability’, ‘cancellation’, etc),
and then access to a back-end where the transactions and data
pertaining to movies is stored. The chat interface channels
are universal and can be used for different kinds of bots. NLP
can be implemented using technologies like AWS Lex or IBM
Watson. The question is: how is the back-end served? Would
you set up a dedicated server (or a cluster of servers), an API
gateway, deploy load balancers, or put in place identity and
access control mechanisms? That’s costly and painful, right!
That’s where serverless technology can help.

The solution is to set up some compute capacity to process
data from a database and also execute this logic in a language
of choice. For example, if you are using the AWS platform,
you can use DynamoDB for the back-end, write programming
logic as Lambda functions, and
expose them through the AWS API
Gateway with a load balancer. This
entire set-up does not require you to
provision any infrastructure or have
any knowledge about underlying
servers/VMs in the cloud. You can
use a database of your choice for
the back-end. Then choose any
programming language supported
in AWS Lambda, including Java,
Python, JavaScript, and C#. There is
no cost involved if there aren’t any
users using the MovieBot. If a blockbuster like ‘Baahubali’ is
released, then there could be a huge surge in users accessing
the MovieBot at the same time, and the set-up would
effortlessly scale (you have to pay for the calls, though).
Phew! You essentially engineered a serverless application.

With this, it’s time to define the term ‘serverless’.
Serverless architectures refer to applications that significantly
depend on third-party services (known as Backend-as-a-
Service or BaaS) or on custom code that’s run in ephemeral
containers (Function-as-a-Service or FaaS).

Hmm, that’s a mouthful of words; so let’s dissect
this description.

* Backend-as-a-Service: Typically, databases (often NoSQL
flavours) hold the data and can be accessed over the cloud,
and a service can be used to help access that back-end.
Such a back-end service is referred to as BaaS.
 
* Function-as-a-Service: Code that processes the requests
(i.e., the ‘programming logic’ written in your favourite
programming language) could be run on containers that are
spun and destroyed as needed. They are known as FaaS.

The word ‘serverless’ is misleading because it literally
means there are no servers. Actually, the word implies, “I don’t
care what a server is.” In other words, serverless enables us
to create applications without thinking about servers, i.e., we
can build and run applications or services without worrying
about provisioning, managing or scaling the underlying
infrastructure. Just put your code in the cloud and run it! Keep
in mind that this applies to Platform-as-a-Service (PaaS) as
well; although you may not deal with direct VMs with PaaS,
you still have to deal with instance sizes and capacity.

Think of serverless as a piece of functionality to run
— not in your machine but executed remotely. Typically,
serverless functions are executed in an ‘event-driven’
fashion — the functions get executed as a response to events
or requests on HTTP. In the case of the MovieBot, the
Lambda functions are invoked to serve user queries as and
when user(s) interact with it.

### Use cases
With serverless architecture, developers can deploy certain
types of solutions at scale with cost-effectiveness. We have
already discussed developing chatbots - it is a classic use
case for serverless computing. Other key use cases for the
serverless approach are given below.

1) Three-tier Web applications: Conventional single page
applications (SPA), which rely on REpresentative State
Transfer (REST) based services to perform a given
functionality, can be re-written to leverage serverless
functions front-ended by an API gateway. This is a
powerful pattern that helps your application scale
infinitely, without concerns of configuring scale-out or
infrastructure resources.

2) Scalable batch jobs: Batch jobs were traditionally run
as daemons or background processes on dedicated VMs.
More often than not, this approach hit scalability and had
reliability issues - developers would leave their critical
processes with Single Points of Failure (SPoF). With the
serverless approach, batch jobs can now be redesigned
as a chain of mappers and reducers, each running as
independent functions. Such mappers and reducers will
share a common data store, something like a blob storage
or a queue, and can individually scale up to meet the data
processing needs.

3) Stream processing: Related to scalable batch jobs is the
pattern of ingesting and processing large streams of data
for near-real-time processing. Streams from services
like Kafka and Kinesis can be processed by serverless
functions, which can be scaled seamlessly to reduce
latency and increase the throughput of the system. This
pattern can elegantly handle spiky loads as well.

4) Automation/event-driven processing: Perhaps the first
application of serverless computing was automation.
Functions could be written to respond to certain alerts
or events. These could also be periodically scheduled to
augment the capabilities for the cloud service provider
through extensibility.

The kind of applications that are best suited for serverless
architectures include mobile back-ends, data processing
systems (real-time and batch) and Web applications.
In general, serverless architecture is suitable for any
distributed system that reacts to events or process workloads
dynamically, based on demand. For example, serverless
computing is suitable for processing events from IoT (Internet
of Things) devices, processing large data sets (in Big Data)
and intelligent systems that respond to queries (chatbots).

### Serverless technologies

There are many proprietary and a few open source serverless
technologies and platforms available for us to choose from.

AWS Lambda is the earliest (announced in late 2014 and
released in 2015) and the most popular serverless technology,
while other players are fast catching up. Microsoft’s Azure

Functions has good support for a wider variety of languages
and integrates with Microsoft’s Azure services. Google’s
Cloud Functions is currently in beta. One of the key
open source players in serverless technologies is Apache
OpenWhisk, backed by IBM and Adobe. It is often tedious
to develop applications directly on these platforms (AWS,
Azure, Google and OpenWhisk). The serverless framework is
a popular solution that aims to ease application development
on these platforms.

Many solutions (especially open source) focus on
abstracting away the details of container technologies like
Docker and Kubernetes. Hyper.sh provides a container
hosting service in which you can use Docker images
directly in serverless style. Kubeless from Bitnami, Fission
from Platform9, and funktion from Fabric8 are serverless
frameworks that provide an abstraction over Kubernetes.

Given that serverless architecture is an emerging approach,
technologies are still evolving and are yet to mature. So you
will see a lot of action in this space in the years to come.

### Challenges in going serverless

Despite the fact that a few large businesses are already
powered entirely by serverless technologies, we should keep
in mind that serverless is an emerging approach. There are
many challenges we need to deal with when developing
serverless solutions. Let us discuss them in the context of the
MovieBot example mentioned earlier.

* Debugging

Unlike in typical application development, there is no
concept of a local environment for serverless functions. Even
fundamental debugging operations like stepping-through,
breakpoints, step-over and watch points are not available with
serverless functions. As of now, we need to rely on extensive
logging and instrumentation for debugging.

When MovieBot provides an inconsistent response or
does not understand the intent of the user, how do we debug
the code that is running remotely? For situations such as this,
we have to log numerous details: NLP scores, the dialogue
responses, query results of the movie ticket database, etc.
Then we have to manually analyse and do detective work to
find out what could have gone wrong. And, that is painful.

* State management

Although serverless is inherently stateless, real-world
applications invariably have to deal with state. Orchestrating
a set of serverless functions becomes a significant challenge
when there is a common context that has to be passed
between them.

Any chatbot conversation represents a dialogue. It
is important for the program to understand the entire
conversation. For example, for the query, “Is ‘Dunkirk’
playing in Urvashi Theatre in Bengaluru tonight?” if the
answer from MovieBot is “Yes”, then the next query from
the user could be, “Are two tickets available?” If MovieBot
confirms this, the user could say, “Okay, book it.” For this
transaction to work, MovieBot should remember the entire
dialogue, which includes the name of the movie, the theatre’s
location, the city, and the number of tickets to book. This
entire dialogue represents a sequence of stateless function
calls. However, we need to persist this state for the final
transaction to be successful. This maintenance of state
external to functions is a tedious task.

* Vendor lock-in

Although we talk about isolated functions that are
executed independently, we are in practice tied to the SDK
(software development kit) and the services provided by
the serverless technology platform. This could result in
vendor lock-in because it is difficult to migrate to other
equivalent platforms.

Let’s assume that we implement the MovieBot on the AWS
Lambda platform using Python. Though the core logic of the
bot is written as Lambda functions, we need to use other related
services from the AWS platform for the chatbot to work, such
as AWS Lex (for NLP), AWS API gateway, DynamoDB (for
data persistence), etc. Further, the bot code may need to make
use of the AWS SDK to consume the services (such as S3 or
DynamoDB), and that is written using boto3. In other words,
for the bot to be a reality, it needs to consume many more
services from the AWS platform than just the Lambda function
code written in plain Python. This results in vendor lock-in
because it is harder to migrate the bot to other platforms.

* Other challenges

Each serverless function code will typically have third
party library dependencies. When deploying the serverless
function, we need to deploy the third party dependency
packages as well, and that increases the deployment package
size. Because containers are used underneath to execute the
serverless functions, the increased deployment size increases
the latency to start up and execute the serverless functions.

Further, maintaining all the dependent packages, versioning
them, etc, is a practical challenge as well.

Another challenge is the lack of support for widely used
languages from serverless platforms. For instance, as of May
2017, you can write functions in C#, Node.js (4.3 and 6.10),
Python (2.7 and 3.6) and Java 8 on AWS Lambda. How about
other languages like Go, PHP, Ruby, Groovy, Rust or any
others of your choice? Though there are solutions to write
serverless functions in these languages and execute them, it
is harder to do so. Since serverless technologies are maturing
with support for a wider number of languages, this challenge
will gradually disappear with time.

Serverless is all about creating solutions without thinking or
worrying about servers; think of it as just putting your code in
the cloud and running it! Serverless is a game-changer because
it shifts the way you look at how applications are composed,
written, deployed and scaled. If you want significant agility
in creating highly scalable applications while remaining
cost-effective, serverless is what you need. Businesses across
the world are already providing highly compelling solutions
using serverless computing technologies. The applications
serverless has range from chatbots to real-time stream
processing from IoT (Internet of Things) devices. So it is not
a question of if, but rather, when you will adopt the serverless
approach for your business.

### References

[1] ‘Build Your Own Technology Radar’, Neal Ford, http://nealford.com/memeagora/2013/05/28/build_your_own_technology_radar.html

[2] ‘Serverless Architectures’, Martin Fowler, https://martinfowler.com/articles/serverless.html

[3] ‘Why the Fuss About Serverless?’ Simon Wardley, http://blog.gardeviance.org/2016/11/why-fuss-about-serverless.html

[4] ‘Serverless Architectural Patterns and Best Practices’,
Amazon Web Services, https://www.youtube.com/watch?v=b7UMoc1iUYw

Serverless technologies
* AWS Lambda: https://aws.amazon.com/lambda/
* Azure Functions: https://functions.azure.com/
* Google Cloud Functions: https://cloud.google.com/
functions/
* Apache OpenWhisk: https://github.com/openwhisk
* Serverless framework: https://github.com/serverless/
serverless
* Fission: https://github.com/fission/fission
* Hyper.sh: https://github.com/hyperhq/
* Funktion: https://funktion.fabric8.io/
* Kubeless: http://kubeless.io/
