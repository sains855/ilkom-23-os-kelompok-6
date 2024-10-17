# PEMBUATAN DAEMON SERVICE SERVER LARAVEL
# Laravel Daemon Service with Supervisor

This guide provides steps to set up **Supervisor** to manage Laravel background processes (such as queue workers and scheduled tasks) as daemon services. This setup ensures these processes run continuously in the background and restart automatically after failures or server reboots.

## Table of Contents
1. [Introduction](#introduction)
2. [Requirements](#requirements)
3. [Installing Supervisor](#installing-supervisor)
4. [Configuring Supervisor for Laravel](#configuring-supervisor-for-laravel)
5. [Managing Supervisor Processes](#managing-supervisor-processes)
6. [Logs and Monitoring](#logs-and-monitoring)
7. [Conclusion](#conclusion)

---

## Introduction

Laravel applications often require background processes for tasks like handling queues, running scheduled jobs, and managing long-running commands. By using **Supervisor**, we can manage these processes as services that start automatically, restart upon failure, and remain active across server reboots.

## Requirements

- A Laravel application running on a Linux-based server (e.g., Ubuntu).
- **Supervisor** installed on the server.

## Installing Supervisor

To install **Supervisor** on your server (Ubuntu):

```bash
sudo apt-get update
sudo apt-get install supervisor
