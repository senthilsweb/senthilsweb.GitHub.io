# Mastering Otel collector - Filelog Receiver: Log Routing & Data Enrichment for Microservices

> This article is a sequel to my earlier post, “Instant Observability with Zero Code!”. In this second part of the series, we dive into more advanced configurations for the Open telemetry collector especially the  filelog receiver for log files routing and data enrichment leveraging router, multiple filelog receivers, regex parsers etc.

Author: Senthilnathan Karuppaiah · Date: 2024-09-08

![Otel Filelog Receiver](/i/blog/Mastering_Otel_collector_banner.jpg)

This article is a sequel to my earlier post, <a href="https://www.linkedin.com/pulse/instant-observability-zero-code-senthilnathan-karuppaiah-k6nqe/?trackingId=afGEpZq%2FQmWv2Owv6OScoA%3D%3D&lipi=urn%3Ali%3Apage%3Ad_flagship3_pulse_read%3BYWGc7XfLTo2r%2BSP3er6wFQ%3D%3D" class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400">“Instant Observability with Zero Code!”</a>. In this second part of the series, we dive into more advanced configurations for the Open telemetry collector especially the  filelog receiver for log files routing and data enrichment leveraging router, multiple filelog receivers, regex parsers etc.

### Modern Applications & Microservices:

![Observability as sidecar](/i/blog/Mastering_Otel_collector_micro_service_1.png)

In today’s world, modern applications are almost always built using heterogeneous technology stacks. With microservices often distributed across different environments and logs scattered across multiple folders, managing and analyzing logs from such complex systems is inevitable. This article provides practical solutions for these challenges, helping you efficiently navigate large-scale applications with diverse logs.


## Source Code:

Make sure to check out the fully working examples that demonstrate how to parse and route logs efficiently across different environments and different log file formats.

Check it out on GitHub: https://github.com/senthilsweb/observability