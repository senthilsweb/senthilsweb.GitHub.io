# Streamlining Data Workflows: How I Use Dagster to Solve Practical Problems for Reliable Data Pipelines.

> I'm sharing a collection of my work in data engineering that showcases practical applications of Dagster for managing and orchestrating data pipelines.

Author: Senthilnathan Karuppaiah · Date: 2024-04-21

![Streamlining Data Workflows](/i/blog/Streamlining-Data-Workflows_banner.png)
I'm sharing a collection of my work in data engineering that showcases practical applications of Dagster for managing and orchestrating data pipelines. Through these examples, you'll discover how <a href="https://dagster.io/" class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400">Dagster</a> helps streamline and optimize various data processes.


In this collection, I've included tasks related to data engineering, and other day-to-day application-related long-running multi-step background tasks. I approach these tasks as "bots," each designed to address a specific problem with a single responsibility. Every bot is meticulously programmed with detailed inline comments explaining the dependencies and enhanced logging for better observability. I adhere to a standard style and convention while programming these bots, ensuring each step is clear and maintainable.


## Why Dagster and why not Airflow?

I prefer using Dagster over other orchestration tools like Airflow for its simplicity and embeddable nature. Dagster is also increasingly popular in modern orchestration platforms, meeting the requirements of the modern data stack with features like Data Catalog, Lineage, Federated Data Governance, and Data Checks/Data Quality, which I discussed in my earlier posts and LinkedIn updates.

### Source code

For those interested in exploring the code and contributing, all resources and project details are available on my <a href='https://github.com/senthilsweb/dagster-data-pipeline' class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400">GitHub</a> repository. You can delve into the codebase, experiment with the implementations, or even contribute to its development.

Visit the GitHub repository <a href='https://github.com/senthilsweb/dagster-data-pipeline' class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400">dagster-data-pipeline.</a>

### Screenshots

![The final result](/i/blog/Streamlining-Data-Workflows-1.png)
<div class="relative flex items-center">The final result</div>

![Pipeline run history](/i/blog/Streamlining-Data-Workflows-2.png)
<div class="relative flex items-center">Pipeline run history</div>

![Lineage vertical](/i/blog/Streamlining-Data-Workflows-3.png)
<div class="relative flex items-center">Lineage vertical</div>

**Disclaimer:** The PDF documents and ebooks used in these demonstrations are intended solely for demonstration purposes. Full access and further usage of these materials are subject to the applicable copyright laws.