SREcon 2019 :: Brooklyn
=======================

My apologies for any missing, misquoted, misleading or otherwise inaccurate
information. I offer this repository to share information gathered at SREcon.

# Table of Contents

  * [My General Notes](#my-general-notes)
  * [Presentations](#presentations)
    * [What Breaks Our Systems: A Taxonomy of Black Swans](#what-breaks-our-systems-a-taxonomy-of-black-swans)
    * [Complexity: The Crucial Ingredient in Your Kitchen](#complexity-the-crucial-ingredient-in-your-kitchen)
    * [Case Study: Implementing SLOs for a New Service](#case-study-implementing-slos-for-a-new-service)
    * [Fixing On-Call When Nobody Thinks It's (Too) Broken](#fixing-on-call-when-nobody-thinks-its-too-broken)
    * [Lessons Learned in Black Box Monitoring 25,000 Endpoints and Proving the SRE Team's Value](#lessons-learned-in-black-box-monitoring-25000-endpoints-and-proving-the-sre-teams-value)
    * [Keeping the Balance: Internet-Scale Loadbalancing Demystified](#keeping-the-balance-internet-scale-loadbalancing-demystified)
    * [Code Yellow: Helping Operations Top-Heavy Teams the Smart Way](#code-yellow-helping-operations-top-heavy-teams-the-smart-way)
    * [How Did Things Go Right? Learning More from Incidents](#how-did-things-go-right-learning-more-from-incidents)
    * [Creating a Code Review Culture](#creating-a-code-review-culture)
    * [Tracing, Fast and Slow: Digging into and Improving Your Web Service's Performance](#tracing-fast-and-slow-digging-into-and-improving-your-web-services-performance)
    * [Visibility Into Loggers](#visibility-into-loggers)
    * [A Guided Tour of Kubernetes Cluster Setup](#a-guided-tour-of-kubernetes-cluster-setup)
    * [What I Wish I Knew before Going On-call](#what-i-wish-i-knew-before-going-on-call)

# My General Notes

* Conference superhero: an HDMI dongle. Presenters and booth squatters, pack laptop connectors and expect the unexpected. Power adapters end up worth their weight in gold. Apple Stores do not conveniently locate themselves close to conferences.
* Code of conduct announcement provided by [Liz Fong-Jones](https://twitter.com/lizthegrey). In short, do not be a jerk.
* Wifi at these types of events tend to suck.
  * If you plan to attend any tech sessions with laptop requirements, I recommend pulling common Docker and virtual machine images down locally, ahead of time.
  * tcpdump told me that the wifi-offered name resolver took a long time to respond with addresses, so I modified my preferences to use Google DNS. Ensure you update those settings before you attempt to get onto hotel wifi, as authentication will likely not work.
* I want art from [Emily Griffin](https://www.daybrighten.com/) for any future slides I need to present from.
* I did not attend the talk, but read about [Amy Tobey](https://twitter.com/missamytobey)'s quote, "Heroes are a liability."
* I missed [Leslie Carr](https://twitter.com/lesliegeek?lang=en)'s [presentation about loving your job](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_carr.pdf). That sounded like a good one.

# Presentations

## What Breaks Our Systems: A Taxonomy of Black Swans

Black swan events: unforeseen, unanticipated, and catastrophic issues. These are the incidents that take our systems down, hard, and keep them down for a long time.

By definition, you cannot predict true black swans. But black swans often fall into certain categories that we've seen before. This talk examines those categories and how we can harden our systems against these categories of events, which include unforeseen hard capacity limits, cascading failures, hidden system dependencies, and more.

### Presenter

[Laura Nolan](https://twitter.com/lauralifts)'s background is in Site Reliability Engineering, software engineering, distributed systems, and computer science. She wrote the 'Managing Critical State' chapter in the O'Reilly 'Site Reliability Engineering' book, as well as contributing to the more recent 'Seeking SRE'.

### Notes

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_nolan.pdf)

#### Select Outages

1. Instapaper [hit a filesystem limitation](https://medium.com/making-instapaper/instapaper-outage-cause-recovery-3c32a7e9cc5f).
1. Sentry [exhausted PostgreSQL transaction IDs](https://blog.sentry.io/2015/07/23/transaction-id-wraparound-in-postgres.html).
1. One company adversely affected by slowed customers sourcing connections from within AWS.
1. An engineer attempting to wipe one rack of hosts' disks ended up wiping the entire CDN fleet, due to a poorly-generated regular expression.

## Complexity: The Crucial Ingredient in Your Kitchen

Software engineering is basically rocket science, so it comes as no surprise that we can learn a lot from that industry. For example, the Challenger explosion in 1986 is a fascinating subject for study. The details of the incident are well documented from a variety of angles (engineering, political, sociotechnical, ethnographical, etc) providing a rich dataset. Highlighting a few examples from this, we can empathize with the architecture considerations and organizational issues that engineers faced at NASA during that time. There are strong, informative parallels between the events that led up to that tragic incident and how software engineers think about reliability today. As Churchill allegedly quipped, "Never let a good crisis go to waste."

[Casey Rosenthal](https://twitter.com/caseyrosenthal), CEO/Founder of Verica.io. Previously an engineering manager for the Traffic Engineering Team and the Chaos Engineering Team at Netflix. As an executive manager and senior architect, Casey has managed teams to tackle Big Data, architect solutions to difficult problems, and train others to do the same. He finds opportunities to leverage his experience with distributed systems, artificial intelligence, translating novel algorithms and academia into working models, and selling a vision of the possible to clients and colleagues alike. For fun, Casey models human behavior using personality profiles in Ruby, Erlang, Elixir, Prolog, Scala, and other languages. He speaks frequently on the topics of Chaos Engineering and Complexity.

### Notes

1. A complex system is one where a single person cannot understand all components' interactions.
1. Adding redundancy can contribute to problems. Spaceshuttle Challenger engineers added a second o-ring when they noticed damage to o-rings during testing.
1. Risk avoidance does not keep systems safer. A study of squirrels found that the groups less likely to get hit by vehicles cross more streets.
1. Accidental accumulation of complexities leads to time spent on clean up, which proves unsustainable.
1. Essential complexity trends at the same rate as requirements, and should not bother anyone.
1. Casey wore a power gauntlet, assumingly to forward his slideshow. When asked by an audience member why he was wearing "Thanos' Glove", he replied, "Gauntlet. And the question is, why aren't we all?" (Quote might not be exact)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_rosenthal.pdf)

## Case Study: Implementing SLOs for a New Service

Implementing service level objectives (SLOs) effectively is a hard task, especially for a service which not only is new within your engineering and product organizations but also encompasses both a request-driven and a storage subsystem.

In this talk, I will discuss our experience defining and measuring service level indicators (SLIs) and objectives for our Ceph Object Storage service. I will describe our approach in specifying service level indicators plus the tradeoffs and implementation decisions we made when it came to measuring various types of SLIs, including availability, latency, and durability.

I will also share the lessons learned and benefits gained from our implementation. You will understand why SLOs are crucial for site reliability engineers and service users and will be given some tips on how to implement them for either a request-driven or a storage system.

### Presenter

[Arnaud Lawson](https://twitter.com/arnolawson) is a Senior Site Reliability Engineer at Squarespace in New York, where—among other things—he has led the productionization of Ceph as a storage backend used by many Squarespace services.

### Notes

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides__lawson.pdf)

## Fixing On-Call When Nobody Thinks It's (Too) Broken

What's a team to do when they receive more than 30 pages a day, every day, for almost a decade? Deny there's a problem of course! Join me as we relive the data-informed journey from around 70,000 pages over 7 years (\~200/week) to under 50/week in just a few short months in a way that shows those carrying the pager improvement is possible and empowers them to continue questioning and improving the status quo moving forward. We'll look at not only the technical challenges but also non-technical challenges like getting buy-in when nobody thinks there's a problem and managing risk when the on-call team is concerned about silencing legitimate pages along with the noise.

### Presenter

Tony Lykke is an SRE on the trade systems team at Hudson River Trading based in NYC, where he gets to tackle hard (often not just technically) automation problems and tech debt cleanup projects across a variety of environments. He is obsessively anti-toil, and regularly refuses to accept "that's just the way it is" as an answer.

### Notes

1. Alerting system silence should not spark investigations to see if anything's wrong.
1. Funnel silenced alerts (and self-remediated issues) into a Slack channel. Their presence offers availability confidence for team members.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_lykke.pdf)

## Lessons Learned in Black Box Monitoring 25,000 Endpoints and Proving the SRE Team's Value

How do you monitor systems that don't want to be monitored or ones that you don't have internal access to? Why monitor these systems at all? The United States Digital Service finds the truth and tells the truth, and fights fires across government, even when those fires don't want to be found. We put together a system to black box monitor all 25,000 .GOV domains and then expanded to perform more robust monitoring of important citizen-facing, government-provided services so we can go where the work is and restore services. In the process, we're hoping to change the culture and prove the value of SRE teams across government. This is how we're doing it.

### Presenter

[Aaron Wieczorek](https://twitter.com/_a12k) is a Site Reliability Engineer at the United States Digital Service Headquarters team. He works on hard technical problems and hard bureaucratic problems, from infrastructure to CI/CD pipelines, to network engineering.

### Notes

1. USDS started in 2014, in the wake of the HealthCare.Gov rollout fiasco.
1. Attempting to provide monitoring and alerting of issues for 25k+ government sites.
1. Leveraging AWS Lambda.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_wieczorek.pdf)

## Keeping the Balance: Internet-Scale Loadbalancing Demystified

Can you explain the entire path that an IP packet takes from your users to your binary? What about a web request? Do you understand the tradeoffs that different kinds of load balancing techniques make? If not, this talk is for you.

Load balancing is hard, and it is made up of many disparate technologies. It cuts across network, transport, and application layers. We'll describe different flavours of load balancing (network, naming, application) and how they are composed together by cloud providers and other large Internet companies to provide fast, reliable, multi-region services.

### Presenters

[Laura Nolan](https://twitter.com/lauralifts)'s (Slack) background is in Site Reliability Engineering, software engineering, distributed systems, and computer science. She wrote the 'Managing Critical State' chapter in the O'Reilly 'Site Reliability Engineering' book, as well as contributing to the more recent 'Seeking SRE'.

[Murali Suriar](https://twitter.com/msuriar) is a lapsed computer science graduate, turned network engineer, turned SRE. Currently working at Google running cluster filesystem and locking services. Left Google to get on a boat. Got bored and came back.

### Notes

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_nolan-load-balancing.pdf)

## Code Yellow: Helping Operations Top-Heavy Teams the Smart Way

We will look at the process for Code Yellow, the term we use for this process of "righting the ship," and discuss how to identify teams that are struggling. Through a look at three separate experiences, we will examine some of the root causes, what steps were taken, and how the engineering organization as a whole supports the process.

### Presenters

[Michael Kehoe](https://www.slideshare.net/MichaelKehoe3) is a Staff SRE at LinkedIn who works on building scalable monitoring infrastructure, reliability principles, and incident management. Michael previously interned at NASA Ames on their PhoneSat project. Michael's key interests lie in network engineering and automation.

[Todd Palino](https://twitter.com/bonkoif) is a Senior Staff Engineer in Site Reliability at LinkedIn on the Capacity Engineering team, where his team is creating a framework for application capacity measurement, analysis, and change intelligence. Prior to that, he was responsible for architecture, day-to-day operations, and tools development for one of the largest Apache Kafka deployments. In his spare time, Todd is the developer of the open source project Burrow, a Kafka consumer monitoring tool, and is the co-author of Kafka: The Definitive Guide, now available from O'Reilly Media. Out of the office, you can find Todd at conferences like SREcon and LISA, sharing his experience from years in SRE technical leadership, and at Kafka Summit or ApacheCon talking about how to feed and water Kafka infrastructures. Or maybe out on the trails, training for the next marathon.

### Notes

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_kehoe.pdf)

[Todd's Slideshare link](https://www.slideshare.net/ToddPalino)

## How Did Things Go Right? Learning More from Incidents

Solely learning from failure isn't a fundamental —- it's a limitation.

A look into the New View of Safety, Human & Organizational Performance, and Resilience Engineering shows us that safety, great performance, and sources of resilience do not come from the absence of failure but rather the presence of adaptive capacity.

Navigating a perfect storm in a world where availability is made up and the 9's don't matter requires expertise. This talk will describe more rewarding ways to approach incident investigation without overly focusing on failure prevention.

* What's going on when it seems like nothing is happening?
* When failure does occur, what's going to keep it from being worse?
* How do teams adapt successfully when preventative techniques fail?
* How should we prioritize the effort to develop systems that help us safely manage the consequences of failure?

These questions cannot be answered by trying to explain the causes of failure and fixing remediation items.

We will move the needle forward and increase our opportunity for learning from success with some fundamental and practical ways that get us from, "Why did things go wrong?" to "How did things go right?"

### Presenter

[Ryan Kitchens](https://twitter.com/this_hits_home) is a Site Reliability Engineer on the Core team at Netflix where he works on building capacity across the organization to ensure its availability and reliability. Before that, Ryan was a founding member of the SRE team at Blizzard Entertainment.

### Notes

1. During incident reviews, focus on 'how' more than 'why'.
1. Engineers often answer 'why' with self-blaming responses; 'how' with stories about the conditions which contributed to their execution decisions.
1. Availability data does not gauge the effort which goes into keeping a system healthy.

[Github - Learning From Incidents](https://github.com/thishitshome/learning-from-incidents)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_kitchens.pdf)

## Creating a Code Review Culture

Code review is one of the best ways to keep code quality high, and for engineering teams to communicate their best practices and patterns. But how do organizations build a sustainable code review culture? This talk explores best practices for introducing code review to teams and looks at how to improve the code review process from the perspective of organizations, code authors, and code reviewers.

### Presenter

[Johnathan Turner](http://twitter.com/while1malloc0) is a Site Reliability Engineer at Squarespace, where he works on tooling and processes that enable product engineers to care less about infrastructure. He spends his spare time playing guitar, reading comic books, listening to heavy metal, and thinking about how to make software more human-centric.

### Notes

Decent [code review checklist](https://github.com/while1malloc0/code-review-checklist) offered.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_turner.pdf)

## Tracing, Fast and Slow: Digging into and Improving Your Web Service's Performance

Do you maintain a Rube Goldberg-like service? Perhaps it's highly distributed? Or you recently walked onto a team with an unfamiliar codebase? Have you noticed your service responds slower than molasses? This talk walks you through how to pinpoint bottlenecks, approaches, and tools to make improvements, and make you seem like the hero! All in a day's work.

The talk will describe various types of tracing a web service, including black & white box tracing, tracing distributed systems, as well as various tools and external services available to measure performance. I also present a few different rabbit holes to dive into when trying to improve your service's performance.

### Presenter

[Lynn Root](https://twitter.com/roguelynn) is an SRE at Spotify in NYC, with historical issues of using her last name as her username, and the resident FOSS evangelist. She is also a global leader of PyLadies and former Vice Chair of the Python Software Foundation Board of Directors. When her hands are not on a keyboard, they are usually holding a bass guitar or a paintbrush.

### Notes

1. OpenTracing: open source solution
1. OpenCensus: open source from Google. More observability than tracing, but useful.
1. Zipkin (Twitter)
1. Jaeger (Uber)
1. X-Ray (AWS)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_root.pdf)

[Other](http://rogue.ly/tracing)

## Visibility Into Loggers

Loggers and tracers have become crucial components of computing systems, providing invaluable visibility into the runtime behavior of our software. Ironically, these vital components are opaque when it comes to their own runtime behavior. We typically only look at logging as suspects in performance-related incidents as part of post-mortem analysis.

Why do we have such blind spots when it comes to components that are pervasively used in our systems? We explore possible explanations and present example solutions.

### Presenter

Danny Chen (Bloomberg) started his career almost 40 years ago as a UNIX performance engineer at Bell Laboratories where he was a co-developer of one of first general purpose UNIX kernel tracing facilities (USENIX/1988: CASPER the Friendly Daemon). He also contributed to the SVR4 virtual memory implementation (USENIX/1990: "Insuring Improved VM Performance - Some No-Fault Policies). Since then he has worked on a wide variety of systems ranging from low latency market data to distributed transaction managers—all while tailing logs

### Notes

1. No Twitter handle. Boo! When asked about that, he said, "I'm an ol' timer."
1. Further reading
  * [History of Fire Escapes](https://www.slideshare.net/TanyaReilly/the-history-of-fire-escapes), by [Tanya Reilly](https://twitter.com/whereistanya)
  * [Antics, Drift and Chaos](https://lorinhochstein.wordpress.com/2017/10/03/antics-drift-and-chaos/), by [Lorin Hochstein](https://twitter.com/lhochstein)
1. Bloomberg [tech blog](http://techatbloomberg.com)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_chen.pdf)

## A Guided Tour of Kubernetes Cluster Setup

A lot of SREs are (or will soon be) responsible for Kubernetes clusters. But what exactly makes up Kubernetes? This talk will dive into the services and systems that make a cluster work, how they interact, and what can go wrong. Kubernetes will no longer be a black box, but a system that can be debugged, reconfigured, and improved to suit every administrators' needs.

### Presenter

[Liz Frost](https://twitter.com/stillinbeta) is a kubernetes contributor and engineer at VMware, née Heptio. She is also a dog mom, queer woman, and occasionally a colorful pony.

### Notes

1. [Instructions](http://bit.ly/srecon-cake0)
1. I [pronounce Kubernetes](https://en.wiktionary.org/wiki/%CE%BA%CF%85%CE%B2%CE%B5%CF%81%CE%BD%CE%AE%CF%84%CE%B7%CF%82#Pronunciation) incorrectly, and might continue to.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_frost.pdf)

## What I Wish I Knew before Going On-call

Firefighting a broken system is time-sensitive and stressful but becomes even more challenging as teams and systems evolve. As an on-call engineer, scaling processes among humans is an important problem to solve. How do we ramp up new engineers effectively? How can we bring existing on-call engineers up to speed? In this workshop we'll share common myths among new on-call engineers and the Do's and Don'ts of on-call onboarding, as well as run through hands-on activities you can take back to work and apply directly to your own on-call processes.

### Presenters

Chie Shu is a backend Software Engineer at Yelp. She has worked on improving Yelp's revenue-critical Ads data pipeline to be more resilient to system failures, and designed heuristics used internally by executives and Product Managers to assess the financial impact of on-call incidents. Chie holds a bachelor's degree in Computational Biology from Cornell University.

Dorothy Jung is a Software Engineer with multiple years of on-call experience. At Yelp she served as a "pushmaster", managing and monitoring company-wide deployments to production; and as a release engineering deputy, helping to set up CI/CD pipelines within the Ads organization. She was previously at DreamWorks Animation R&D, where she worked on upgrading the studio's build management tools. Dorothy holds a bachelor's degree in Computer Science and French from the University of California, Berkeley.

Wenting Wang is a Software Engineer with three years of industry experience. She has been on-call for different teams at Yelp: on the BizApp backend team, where she worked closely with mobile developers and monitored mobile user traffic; and on the Ads team, where she currently develops and maintains revenue-critical real-time processing systems. Wenting received her master's degree in Computer Science from Shanghai Jiao Tong University and was previously a doctoral candidate in Computer Science focusing on distributed systems at the University of Illinois at Urbana-Champaign.

### Notes

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/srecon19americas_slides_wang.pdf)

[More info](https://github.com/wentingwang/SRECon19)

[More info](https://github.com/dorothyjung/lisa18)

