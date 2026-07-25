# Running a Binary in Headless Mode

> Running a binary in headless mode can be a useful technique when you need to run a binary on a remote server or in a terminal environment. By running the binary without a graphical user interface (GUI), you can save system resources and ensure that the binary runs smoothly. In this blog post, we'll explore how to run a binary in headless mode using the command line. We'll cover the steps involved in running the binary, verifying that it's running, and stopping it when necessary.

Author: Senthilnathan Karuppaiah · Date: 2023-09-24

## Introduction

Running a binary in headless mode can be a useful technique when you need to run a binary on a remote server or in a terminal environment. By running the binary without a graphical user interface (GUI), you can save system resources and ensure that the binary runs smoothly. In this blog post, we'll explore how to run a binary in headless mode using the command line. We'll cover the steps involved in running the binary, verifying that it's running, and stopping it when necessary.

## Prerequisites

- A binary file that you want to run.
- A terminal environment.

## Step 1: Navigate to the Binary Directory

Navigate to the directory where the binary file is located using the `cd` command. For example, if your binary file is located in the `/usr/local/bin` directory, you can navigate to it using the following command:

```bash
cd /usr/local/bin
```

## Step 2: Run the Binary in Headless Mode
To run the binary in headless mode, you can use the following command:

```bash
nohup ./binary-name > output.log 2>&1 &
```

This command does the following:

- `nohup`: Runs the binary in the background and prevents it from being terminated when the terminal is closed.
- `./binary-name`: Specifies the name of the binary file that you want to run.
- `> output.log`: Redirects the output of the binary to a file named `output.log`.
- `2>&1`: Redirects the error output of the binary to the same file as the standard output.
- `&`: Runs the command in the background.

## Step 3: Verify the Binary is Running
To verify that the binary is running, you can use the following command:

This command lists all running processes and filters the output to show only the processes that contain the name of the binary file. If the binary is running, you should see its process ID (PID) in the output.

```bash
ps aux | grep binary-name
```

## Step 4: Stop the Binary
To stop the binary, you can use the following command:

```bash
kill <pid>
```

Replace `<pid>` with the PID of the binary process that you want to stop. You can obtain the PID using the `ps aux | grep binary-name` command.