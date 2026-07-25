# Deploying Pentaho Carte Server on Fly.io with Firecracker VM: A Fun Way to Learn ETL!

> This article is a sequel to my earlier post, “Instant Observability with Zero Code!”. In this second part of the series, we dive into more advanced configurations for the Open telemetry collector especially the  filelog receiver for log files routing and data enrichment leveraging router, multiple filelog receivers, regex parsers etc.

Author: Senthilnathan Karuppaiah · Date: 2024-09-30

![Be Part of Next Public Cloud](/i/blog/Deploying-Pentaho-Carte-Server-on-Flyio_banner.png)

This is a quick guide on deploying the **Pentaho Carte Server** on <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="http://fly.io/">Fly.io</a> using **Firecracker VM**—a great way to learn and practice the Pentaho data platform with the Pentaho Data Integration **carte** server.

**Carte** is a lightweight web container that allows you to set up a dedicated, remote ETL server, making it easier to manage and execute Pentaho jobs.

**Firecracker** is a lightweight virtualization technology designed to run microVMs (micro virtual machines) efficiently. <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="http://fly.io/">Fly.io</a> is a platform that allows you to deploy applications globally with minimal latency, utilizing Firecracker for fast, scalable deployment. It’s important to note that Firecracker is not Docker; it offers a different approach to virtualization, emphasizing speed and resource efficiency.

Why <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="http://fly.io/">Fly.io</a> is Perfect for Learning and Practicing Pentaho Data Integration?

::list{type="success"}
- **Great for Learning:** Ideal for small workloads and learning projects.
- **Free $5 Credit:** Start deploying with no upfront costs.
- **MicroVMs, Not Docker:** Enjoy lightweight, efficient microVM technology.
- **Effortless Scaling:** Easily scale VMs as your needs grow.
- **One-Command Install:** Run flyctl launch to set up the server quickly.
- **Free HTTPS:** Secure your apps without extra charges.
- **Additional Storage:** Mount extra volumes when needed.
- **Automatic Shutdown:** Save resources when not in use.
- **Rapid Setup:** Machines provision quickly, enabling fast deployment.
::

**Ready to install Pentaho Carte on <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="http://fly.io/">Fly.io</a>**? Check out my Github repository: 

🔗 <a class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400" href="https://github.com/senthilsweb/learn-pentaho-with-senthil">Learn Pentaho with Senthil</a>