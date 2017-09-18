

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
