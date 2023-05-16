---
theme: seriph
background: none
fonts:
  sans: 'Roboto'
  serif: 'Roboto Slab'
  mono: 'Fira Code'
layout: default
css: unocss
favicon: https://opentelemetry.io/favicons/favicon.ico
addons:
  - slidev-addon-components
---

# Pizza Party!!

<img class="center" v-click src="/assets/pizzaparty.webp" />

<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

---
layout: cover
---

# What is Observability

<!--
-->

---
layout: image-left
image: 'https://forbesroad.org/wp-content/uploads/2020/02/ERT1.jpg'
---
# Backstory

One of my first projects, I built and maintained a desktop application, I would build, ship and forget, I had no contact with customers and no need to diagnose their problems.


<!-- 
* Started building a cloud-enabled collaboration addition to the desktop client, suddenly, managed our deployed code, no longer commit and forget.
* On launch, after months of building, I get 5am call from CEO, users aren't getting their emails, 
 -->

---
layout: fact
---

# So, what _is_ Observability™️ ?

Characteristics of a system that allow us to understand it from the outside by asking questions without having to know its inner workings.

---
layout: center
---

# Scenario

<video src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExNjllMzgxMzE3M2I2ZWFlOGUyZDlkMGE4ZTgyYjBlMDE0MjM1NGViYSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/wTDjZPnq6QsAo/giphy.mp4" autoplay loop /><p><a href="https://giphy.com/gifs/the-simpsons-license-plate-bort-wTDjZPnq6QsAo">via GIPHY</a></p>


---
layout: image-right
image: /assets/appInsights.png
---

 # Metrics
![Dashboard](https://www.axamit.com/static/media/hchk3.png)


---
layout: image-left
image: 'https://www.ixbt.com/cpu/intel-thermal-features/c2xeq_8.png'
---
# Metrics

📈 Pre-aggregated metrics for my systems

🕵️ Show all important stats about CPU, RAM, Messages in the queue

<v-click>
🙃 Service? Instance? Method? Request information?
</v-click>

---
title: Logging
layout: image-right
image: 'https://mattionline.de/wp-content/uploads/2020/07/access-log-datei-riesig-nginx.png'
---

# Logging

* Text message added during development
* Lightweight
* Human Readable

---
layout: image
---

![Jurassic Park](/assets/Jurassic-Park-poop-955281948.jpg)

---
layout: image
---
![Grep tail](https://www.evemilano.com/wp-content/uploads/2021/03/tail-grep.png)

<!-- 
You cannot find a message related to the issue, everything looks OK, but you have an idea of where it might be
 -->
---
layout: default
---

```csharp {monaco}
public async Task<string?> GetScheduledEventToken(Type eventType, string entityId, CancellationToken cancellationToken)
{
    var item = await _repo.GetItemAsync(eventType.FullName, entityId, cancellationToken);
    return item?.EventToken;
}
```

<!-- 
With your background you _feel_ this method might be where things are going wrong, but there's no logging there, so, you add some.

Now, you have to build and re-deploy.
 -->

---
layout: image
image: '/assets/deployment_pipeline.png'
---
<img v-click src="/assets/deploy_time.png" />

---
layout: image
image: 'https://cdn-images-1.medium.com/v2/resize:fit:2000/1*pSguAIk9W0FLFVttBxIsPA.png'
---

---
layout: quote
title: That happens
---
> "Oh that happens sometimes, you can just ignore it"
>
> --- you

---
layout: section
---

# The problems

---

# Metrics

* Aggregation removes plenty of data
* If you want more dimensions you have to instrument your code
* Tooling makes it very expensive to have dynamic graphs

<img src="/assets/graphs_many.png" style="max-with:50%" />

---

# Logs

* They're verbose and hard to parse
* Plain-text

<img src="/assets/the-birth-of-lincoln-logss-featured-photo.jpg" style="max-with:50%" />

<!-- 
* We added CorrelationIDs to logs to try and mitigate the issue, but tooling isn't in place
 -->

---

# Lack of context

We don't have a way to relate logs or metrics with the end user and across eachother

---
layout: two-cols
---

# Distributed architectures

![Message flow in microservices](/assets/microservices.gif)

::right::

* [OpenTracing](https://opentracing.io) was started as an incubation project in the CNCF on Oct 2016, it defined a vendor-neutral API specification for sending telemetry.

* [OpenCensus](https://opencensus.io/) provided a set of language-specific libraries for developers to instrument their systems and send it to their backends.

---
layout: center
---

# Same ideals

![Obligatory XKCD](https://imgs.xkcd.com/comics/standards.png)

---
layout: quote
---

# Open Telemetry

> OTel’s goal is to provide a set of standardized vendor-agnostic SDKs, APIs, and [tools](https://opentelemetry.io/docs/collector) for ingesting, transforming, and sending data to an Observability back-end (i.e. open source or commercial vendor)[^1]

![Open Telemetry logo](/assets/opentelemetry.png)

[^1]: [What is Open Telemetry](https://opentelemetry.io/docs/what-is-opentelemetry/)


<!-- 
The community realized they were working towards the same goal and joined together, creating the OpenTelemetry (OTel) project in May 2019,
 -->

---

 # How

 Collect rich signals like _traces_, _metrics_, and _logs_.

 ## Traces

A trace is a representation of the path taken by a request as it propagates through a system


---
layout: section
---

# How does it look

Demo!

---

# Spans

* Represent a Unit of Work or an operation.
* Show the start and end times
* Operation name, events and links
* Any other metadata we want to include
* Established naming convention for standard components
  * db, net, http, etc.

---

# Spans

<table>
  <tr><th>Key</th><th>Value</th></tr>
  <tr><td>net.transtpor</td><td>IP.TCP</td></tr>
  <tr><td>net.peer.ip</td><td>10.224.0.1</td></tr>
  <tr><td>net.peer.port</td><td>443</td></tr>
  <tr><td>net.host.name</td><td>localhost</td></tr>
  <tr><td>http.method</td><td>PUT</td></tr>
  <tr><td>http.target</td><td>/reservation</td></tr>
</table>

---

# Span events

They represent a specific information point that happened during the execution of a span, think of them as log messages in relation to a span.


# Span Links
What about spans that are triggered asynchronously by a trace? Batch processes? Span Links let us relate spans and traces to others.

---

# How does this help us?


* Rich data allows dynamic visualizations and queries after the fact
* The richer the data, the more questions we'll be able to answer
* Start tackling the unknown-unknowns

---
layout: section
---

# What next?

---
layout: quote
---

# Service Level Objectives

> SLOs are the API of your development team
>
> -- Charity Majors (Honeycomb CTO)

---

# Define expectations

* What's the importance of this functionality
* What can other departments expect from our work
* What are experience we offering our end-users