# Flog: A Powerful Fake Log Generator by @mingrammer 🚀📊

> Looking for a simple way to generate fake log data for testing or simulating real-world scenarios?. Look no further than Flog by @mingrammer

Author: Senthilnathan Karuppaiah · Date: 2024-09-09

![Flog](/i/blog/Flog_A_Powerful_Fake_Log_Generator_banner.png)


Looking for a simple way to generate fake log data for testing or simulating real-world scenarios? Look no further than Flog by <a href="https://github.com/mingrammer/flog" class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400">@mingrammer!</a>

Flog supports multiple common log formats like Apache, JSON, and Common Log Format, making it versatile for various use cases. Whether you're testing log management systems, benchmarking, or generating synthetic data, Flog has you covered.

**Best of all**, it's available as a single Golang binary or can be run directly from Docker, giving you flexibility based on your setup. Personally, I like to use it inside a simple shell script to append logs to the local disk:


## Log generator in a shell script

```javascript
# flog.sh
while true; do docker run --rm mingrammer/flog -s 10s -n 20 -f json >> flog.log; sleep 10; done
```

## Generate logs:

Explore Flog on GitHub: Flog - <a href="https://github.com/mingrammer/flog" class="dark:text-teal-400 relative transition hover:text-teal-500 dark:hover:text-teal-400"> Fake Log Generator</a>

```javascript
sh flog.sh
```