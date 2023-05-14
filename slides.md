---
theme: seriph
background: 'https://source.unsplash.com/collection/94734566/1920x1080'
class: text-center
fonts:
  sans: 'Roboto'
  serif: 'Roboto Slab'
  mono: 'Fira Code'
layout: intro
css: unocss
favicon: https://opentelemetry.io/favicons/favicon.ico
addons:
  - slidev-addon-components
---

# What is Observability

<!--
-->

---
transition: fade-out
title: Table of Contents
hideInToc: true
---

<Toc></Toc>

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

# So, what _is_ Observability™️ ?

Observability is a characteristics of a system that allow us to understand it from the outside by asking questions without having to know its inner workings.

---
clicks: 2
---

# Scenario

<show-hide show="1" hide="2">
    <video src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExNjllMzgxMzE3M2I2ZWFlOGUyZDlkMGE4ZTgyYjBlMDE0MjM1NGViYSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/wTDjZPnq6QsAo/giphy.mp4" autoplay loop="false" /><p><a href="https://giphy.com/gifs/the-simpsons-license-plate-bort-wTDjZPnq6QsAo">via GIPHY</a></p>
</show-hide>

<div v-click="2">
    <img src=/assets/image.png/>
</div>



---
title: Logging
---

# Logging

* They record a text message that the developer deems could provide insights when researching an issue
* Lightweight
* Human Readable

---
clicks: 4
---

# Logging


<img show-hide show="1" hide="2" alt="screenshot of a console with log output" v-click src="https://www.evemilano.com/wp-content/uploads/2021/03/tail-grep.png" />

<img show-hide show="3" hide="4" src="/assets/Jurassic-Park-poop-955281948.jpg" />


<div v-click="4">
```csharp {monaco-diff}
public async Task<string?> GetScheduledEventToken(Type eventType, string entityId, CancellationToken cancellationToken)
{
    var item = await _repo.GetItemAsync(eventType.FullName, entityId, cancellationToken);
    return item?.EventToken;
}
```
</div>


---
layout: image-right
transition: none
image: https://www.axamit.com/static/media/hchk3.png
---

 # Monitoring

 <div v-click>📈 Look at all my nice dashboards!</div>
 <div v-click>🕵️ Catch things before end-users notice</div>

---
layout: quote
title: That happens
---
<quote>"Oh that happens sometimes, you can just ignore it"</quote>

---

# Lack of context

We don't have a way to relate logs or metrics with the end user

---
layout: two-cols
---
## Logs

* They're verbose and hard to parse
* Structured logs help add context
* If you didn't add a log then you won't be able to 

::right::

## Metrics

* Aggregation removes plenty of data
* If you want more dimensions you have to instrument your code
* Tooling makes it very expensive to have dynamic graphs

<!-- 
* We added CorrelationIDs to logs to try and mitigate the issue, but tooling isn't in place
 -->

---
layout: two-cols
---

# Distributed architectures

![Message flow in microservices](/assets/microservices.gif)

::right::

* [OpenTracing](https://opentracing.io) was started as an incubation project in the CNCF on Oct 2016, it defined a vendor-neutral API specification for sending telemetry.

* [OpenCensus](https://opencensus.io/) provided a set of language-specific libraries for developers to instrument their systems and send it to their backends.

---

# Same ideals

![Obligatory XKCD](https://imgs.xkcd.com/comics/standards.png)

---

# Open Telemetry

> OTel’s goal is to provide a set of standardized vendor-agnostic SDKs, APIs, and [tools](https://opentelemetry.io/docs/collector) for ingesting, transforming, and sending data to an Observability back-end (i.e. open source or commercial vendor)[^1]

![Open Telemetry logo](/assets/opentelemetry.png)

[^1]: [What is Open Telemetry](https://opentelemetry.io/docs/what-is-opentelemetry/)

<style>
    .footnotes-sep {
    @apply mt-20 opacity-10;
    }
    .footnotes {
    @apply text-sm opacity-75;
    }
    .footnote-backref {
    display: none;
    }
</style>


<!-- 
The community realized they were working towards the same goal and joined together, creating the OpenTelemetry (OTel) project in May 2019,
 -->

 ---

 # How

 Collect rich signals like _traces_, _metrics_, and _logs_.

 ## Traces



