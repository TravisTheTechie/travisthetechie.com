---
layout: post
title: How Do I Load Balance - MassTransit Problems
categories: [code]
tags: [MassTransit]
description: Load balancing is a problem that comes up on the mailing list from time to time. Depending on which transport you use, you options for load balancing differ.
---

Load balancing is a problem that comes up on the mailing list from time to time. Depending on which transport you use, you options for load balancing differ.

With&nbsp;<a href="http://en.wikipedia.org/wiki/Microsoft_Message_Queuing" target="_blank">MSMQ</a>, there's a construct called the&nbsp;<a href="http://masstransit.readthedocs.org/en/master/advanced/distributor.html" target="_blank">distributor</a>. That's the primary way to do load balancing. It will send a small number of messages to each end point registered - enough to fill up all threads and a couple extra so it doesn't sit waiting. The distributor will hold back additional messages so no one endpoint gets filled up, holding messages back. See the distributor sample in the&nbsp;<a href="https://github.com/MassTransit/MassTransit" target="_blank">GitHub repo</a>&nbsp;for an example of this working.

With RabbitMQ you have the option of <a href="http://www.enterpriseintegrationpatterns.com/CompetingConsumers.html" target="_blank">competing consumers</a>. This would be the preferred way to do it. And it's more transparent to your application. You just scale the consumers sideways and it Just Works(TM). You do need to make sure the different consumers work off the same queue and are effectively the same code. No additional code is needed to support this.

Now there's the thought of load balancing the queueing system itself. MSMQ only has the option of clustering the machines. RabbitMQ has some <a href="http://www.rabbitmq.com/ha.html" target="_blank">High Availability</a>&nbsp;options which can be enabled by adding ?ha=true to the queue URI (in pre RabbitMQ 3.0) or by policy in the RabbitMQ server configuration (RabbitMQ 3.0+). RabbitMQ can be clustered to support this behaviour.

Updated: RabbitMQ HA options were old. My clustered RMQ isn't 3.0 yet...