SREcon 2019 :: Brooklyn
=======================

My apologies for any missing, misquoted, misleading or otherwise inaccurate
information. I offer this repository to share information gathered at SREcon.

# Table of Contents

  * [Presentations](#presentations)
    * [What Breaks Our Systems: A Taxonomy of Black Swans](#what-breaks-our-systems-a-taxonomy-of-black-swans)
    * [Complexity: The Crucial Ingredient in Your Kitchen](#complexity-the-crucial-ingredient-in-your-kitchen)
    * [Case Study: Implementing SLOs for a New Service](#case-study-implementing-slos-for-a-new-service)
    * [Fixing On-Call When Nobody Thinks It's (Too) Broken](#fixing-on-call-when-nobody-thinks-its-too-broken)
    * [Lessons Learned in Black Box Monitoring 25,000 Endpoints and Proving the SRE Team's Value](#lessons-learned-in-black-box-monitoring-25000-endpoints-and-proving-the-sre-teams-value)

# Presentations

## What Breaks Our Systems: A Taxonomy of Black Swans

Black swan events: unforeseen, unanticipated, and catastrophic issues. These are the incidents that take our systems down, hard, and keep them down for a long time.

By definition, you cannot predict true black swans. But black swans often fall into certain categories that we've seen before. This talk examines those categories and how we can harden our systems against these categories of events, which include unforeseen hard capacity limits, cascading failures, hidden system dependencies, and more.

Laura Nolan's background is in Site Reliability Engineering, software engineering, distributed systems, and computer science. She wrote the 'Managing Critical State' chapter in the O'Reilly 'Site Reliability Engineering' book, as well as contributing to the more recent 'Seeking SRE'.

[Laura Nolan](https://twitter.com/lauralifts) / [Slack](https://slack.com/)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_nolan.pdf)

## Complexity: The Crucial Ingredient in Your Kitchen

Software engineering is basically rocket science, so it comes as no surprise that we can learn a lot from that industry. For example, the Challenger explosion in 1986 is a fascinating subject for study. The details of the incident are well documented from a variety of angles (engineering, political, sociotechnical, ethnographical, etc) providing a rich dataset. Highlighting a few examples from this, we can empathize with the architecture considerations and organizational issues that engineers faced at NASA during that time. There are strong, informative parallels between the events that led up to that tragic incident and how software engineers think about reliability today. As Churchill allegedly quipped, "Never let a good crisis go to waste."

CEO/Founder of Verica.io. Previously an engineering manager for the Traffic Engineering Team and the Chaos Engineering Team at Netflix. As an executive manager and senior architect, Casey has managed teams to tackle Big Data, architect solutions to difficult problems, and train others to do the same. He finds opportunities to leverage his experience with distributed systems, artificial intelligence, translating novel algorithms and academia into working models, and selling a vision of the possible to clients and colleagues alike. For fun, Casey models human behavior using personality profiles in Ruby, Erlang, Elixir, Prolog, Scala, and other languages. He speaks frequently on the topics of Chaos Engineering and Complexity.

[Casey Rosenthal](https://twitter.com/caseyrosenthal) / Verica.io

## Case Study: Implementing SLOs for a New Service

Implementing service level objectives (SLOs) effectively is a hard task, especially for a service which not only is new within your engineering and product organizations but also encompasses both a request-driven and a storage subsystem.

In this talk, I will discuss our experience defining and measuring service level indicators (SLIs) and objectives for our Ceph Object Storage service. I will describe our approach in specifying service level indicators plus the tradeoffs and implementation decisions we made when it came to measuring various types of SLIs, including availability, latency, and durability.

I will also share the lessons learned and benefits gained from our implementation. You will understand why SLOs are crucial for site reliability engineers and service users and will be given some tips on how to implement them for either a request-driven or a storage system.

Arnaud is a Senior Site Reliability Engineer at Squarespace in New York, where—among other things—he has led the productionization of Ceph as a storage backend used by many Squarespace services.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides__lawson.pdf)

## Fixing On-Call When Nobody Thinks It's (Too) Broken

What's a team to do when they receive more than 30 pages a day, every day, for almost a decade? Deny there's a problem of course! Join me as we relive the data-informed journey from around 70,000 pages over 7 years (\~200/week) to under 50/week in just a few short months in a way that shows those carrying the pager improvement is possible and empowers them to continue questioning and improving the status quo moving forward. We'll look at not only the technical challenges but also non-technical challenges like getting buy-in when nobody thinks there's a problem and managing risk when the on-call team is concerned about silencing legitimate pages along with the noise.

Tony is an SRE on the trade systems team at Hudson River Trading based in NYC, where he gets to tackle hard (often not just technically) automation problems and tech debt cleanup projects across a variety of environments. He is obsessively anti-toil, and regularly refuses to accept "that's just the way it is" as an answer.

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_lykke.pdf)

## Lessons Learned in Black Box Monitoring 25,000 Endpoints and Proving the SRE Team's Value

How do you monitor systems that don't want to be monitored or ones that you don't have internal access to? Why monitor these systems at all? The United States Digital Service finds the truth and tells the truth, and fights fires across government, even when those fires don't want to be found. We put together a system to black box monitor all 25,000 .GOV domains and then expanded to perform more robust monitoring of important citizen-facing, government-provided services so we can go where the work is and restore services. In the process, we're hoping to change the culture and prove the value of SRE teams across government. This is how we're doing it.

Aaron is a Site Reliability Engineer at the United States Digital Service Headquarters team. He works on hard technical problems and hard bureaucratic problems, from infrastructure to CI/CD pipelines, to network engineering.

[Aaron Wieczorek](https://twitter.com/_a12k) / United States Digital Services (USDS)

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_wieczorek.pdf)

## Keeping the Balance: Internet-Scale Loadbalancing Demystified

Can you explain the entire path that an IP packet takes from your users to your binary? What about a web request? Do you understand the tradeoffs that different kinds of load balancing techniques make? If not, this talk is for you.

Load balancing is hard, and it is made up of many disparate technologies. It cuts across network, transport, and application layers. We'll describe different flavours of load balancing (network, naming, application) and how they are composed together by cloud providers and other large Internet companies to provide fast, reliable, multi-region services.

Laura Nolan's background is in Site Reliability Engineering, software engineering, distributed systems, and computer science. She wrote the 'Managing Critical State' chapter in the O'Reilly 'Site Reliability Engineering' book, as well as contributing to the more recent 'Seeking SRE'.

Murali Suriar is a lapsed computer science graduate, turned network engineer, turned SRE. Currently working at Google running cluster filesystem and locking services. Left Google to get on a boat. Got bored and came back.

[Laura Nolan](https://twitter.com/lauralifts) / Slack

[Murali Suriar](https://twitter.com/msuriar) / Google

[Slides](https://www.usenix.org/sites/default/files/conference/protected-files/sre19amer_slides_nolan-load-balancing.pdf)

