# Datadog Windows Agent Installation

## 1. What is Datadog Agent?

The **Datadog Agent** is software installed on a host that collects metrics, logs, traces, and other monitoring data and sends them to Datadog. ([Datadog Monitoring][1])

---

## 2. Windows Agent Installation

### Prerequisites

* Windows host
* Datadog account
* Datadog **API Key**
* Administrator privileges
* Internet connectivity to Datadog

### Step 1 — Download Agent

Download the latest **Datadog Windows Agent MSI** from Datadog.

[Datadog Windows Agent Documentation](https://docs.datadoghq.com/agent/supported_platforms/windows/?utm_source=chatgpt.com)

### Step 2 — Run Installer

1. Download the `.msi` installer.
2. Right-click → **Run as administrator**.
3. Accept the license agreement.
4. Enter your **Datadog API Key**.
5. Complete the installation.

The default installation directory is:

```text
C:\Program Files\Datadog\Datadog Agent
```

The main configuration directory is:

```text
C:\ProgramData\Datadog
```

`ProgramData` is a hidden Windows folder. ([Datadog Monitoring][2])

---

## 3. Important Configuration Files

### Main Agent Configuration

```text
C:\ProgramData\Datadog\datadog.yaml
```

This contains important settings such as:

```yaml
api_key: <DATADOG_API_KEY>
site: datadoghq.com
```

The API key associates the Agent with your Datadog organization. ([Datadog Monitoring][1])

### Agent Logs

```text
C:\ProgramData\Datadog\logs\agent.log
```

Use this file when troubleshooting Agent issues. ([Datadog Monitoring][2])

---

# 4. Verify Agent Installation

Open **PowerShell as Administrator**.

Run:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

This displays the Agent status and integration/check information. ([Datadog Monitoring][2])

You can also check:

```text
Windows Services
      ↓
Datadog Agent
      ↓
Status: Running
```

The Agent runs as the Windows `DatadogAgent` service. ([Datadog Monitoring][2])

---

# 5. Datadog Agent Manager

Windows provides a graphical **Datadog Agent Manager**.

Run:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" launch-gui
```

It opens locally at:

```text
http://127.0.0.1:5002
```

From the Agent Manager you can:

* Check Agent status
* View checks
* Configure integrations
* Restart Agent
* View troubleshooting information
* Send a support flare ([Datadog Monitoring][3])

---

# 6. Windows Agent Troubleshooting

## Problem 1 — Agent is not running

Check the service:

```text
Services
 → Datadog Agent
```

Or run:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

Restart:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" restart-service
```

---

## Problem 2 — Host is not appearing in Datadog

Check:

### 1. Agent status

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

### 2. API Key

Verify:

```text
C:\ProgramData\Datadog\datadog.yaml
```

Check that the API key belongs to the correct Datadog organization.

### 3. Datadog Site

Verify the configured `site` matches your Datadog organization.

### 4. Network connectivity

Make sure the Windows host can reach Datadog through the internet/proxy.

These are among Datadog's recommended first troubleshooting checks. ([Datadog Monitoring][4])

---

# 7. Problem — Metrics Are Not Appearing

Check the Agent status:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

Then check:

```text
C:\ProgramData\Datadog\logs\agent.log
```

Look for:

```text
ERROR
WARN
API
Connection
Authentication
Check
```

Also verify that you restarted the Agent after changing YAML configuration. ([Datadog Monitoring][4])

---

# 8. Troubleshoot a Specific Integration

For example, if a Windows integration/check is failing:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" check <CHECK_NAME>
```

Example:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" check windows
```

The exact check name depends on the integration. ([Datadog Monitoring][5])

---

# 9. Common Troubleshooting Checklist

```text
Datadog Windows Agent Troubleshooting
             |
             ↓
1. Is Datadog Agent service Running?
             |
             ↓
2. Check Agent status
             |
             ↓
3. Verify API Key
             |
             ↓
4. Verify Datadog Site
             |
             ↓
5. Check Internet / Proxy
             |
             ↓
6. Check agent.log
             |
             ↓
7. Check integration status
             |
             ↓
8. Restart Agent
             |
             ↓
9. Generate Agent Flare if required
```

Datadog specifically recommends checking connectivity/proxy, API key, site configuration, duplicate Agents, configuration changes/restarts, Agent status, and logs when troubleshooting. ([Datadog Monitoring][4])

### Interview Quick Revision

**Q: Where is the Datadog Windows configuration file?**
`C:\ProgramData\Datadog\datadog.yaml`

**Q: Where are Agent logs?**
`C:\ProgramData\Datadog\logs\agent.log`

**Q: How do you check Agent status?**
`agent.exe status`

**Q: How do you restart the Agent?**
`agent.exe restart-service`

**Q: How do you troubleshoot an integration?**
`agent.exe check <CHECK_NAME>`

**Q: What are the first things you check when the host doesn't appear in Datadog?**
**Agent status → API key → Datadog site → network/proxy → logs.**

[1]: https://docs.datadoghq.com/getting_started/agent/?utm_source=chatgpt.com "Getting Started with the Agent"
[2]: https://docs.datadoghq.com/agent/supported_platforms/windows/?utm_source=chatgpt.com "Windows"
[3]: https://docs.datadoghq.com/agent/guide/datadog-agent-manager-windows/?utm_source=chatgpt.com "Datadog Agent Manager for Windows"
[4]: https://docs.datadoghq.com/agent/troubleshooting/?utm_source=chatgpt.com "Agent Troubleshooting"
[5]: https://docs.datadoghq.com/agent/troubleshooting/agent_check_status/?lang_pref=en&utm_source=chatgpt.com "Troubleshoot an Agent Check"

## Datadog — Host Infrastructure View

After installing and successfully starting the **Datadog Agent** on a Windows server, the host should appear in Datadog's **Infrastructure → Hosts** view once the Agent starts sending data.

### Steps

1. Install the **Datadog Agent** on the Windows host.
2. Start the **Datadog Agent** service.
3. Verify the Agent:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

4. Log in to Datadog.
5. Go to:

```text
Infrastructure
   ↓
Hosts
```

6. Search for your Windows host.

### What you can see in Host Infrastructure

The host page can provide information such as:

* Hostname
* Operating system
* CPU utilization
* Memory utilization
* Disk usage
* Network activity
* Processes
* Tags
* Metrics
* Agent information
* Integrations/checks

### Basic troubleshooting flow

```text
Windows Server
      ↓
Datadog Agent Installed
      ↓
Agent Service Running
      ↓
API Key + Datadog Site Valid
      ↓
Network Connectivity
      ↓
Agent Sends Data
      ↓
Datadog
      ↓
Infrastructure → Hosts
      ↓
Windows Host
```

### If the host does NOT appear

Check in this order:

```text
1. Agent service
2. agent status
3. API key
4. Datadog site
5. Network / Proxy
6. agent.log
7. Hostname
```

**Key note:** Installing the Agent alone doesn't guarantee that the host will appear; the Agent must be able to authenticate and communicate with Datadog successfully.

For your Datadog notes, there are **two related but different approaches** on Windows: **Live Process Monitoring** for real-time process visibility, and the **Processes integration/process check** for monitoring specific processes and their resource usage. ([Datadog Monitoring][1])

# Datadog — Process Monitoring on Windows

## 1. Enable Live Process Monitoring

The Datadog Agent can collect information about processes running on the Windows host.

### Step 1 — Edit `datadog.yaml`

Location:

```text
C:\ProgramData\Datadog\datadog.yaml
```

Add/enable:

```yaml
process_config:
  process_collection:
    enabled: true
```

Datadog's current Windows documentation uses `process_collection.enabled` for Live Processes. ([Datadog Monitoring][1])

### Step 2 — Restart Datadog Agent

Run PowerShell as Administrator:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" restart-service
```

### Step 3 — Verify

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" status
```

Check that the Process Agent/process collection is running correctly.

---

# 2. View Processes in Datadog

In Datadog:

```text
Infrastructure
   ↓
Processes
```

**Live Processes** provides real-time visibility into processes running on hosts and allows you to examine resource consumption at the process level. ([Datadog Monitoring][1])

You can investigate things such as:

```text
Process
   ↓
CPU
Memory
I/O
Threads
Host
```

---

# 3. Monitor a Specific Process

If you want to monitor a particular application/process, you can use the **Processes integration / Process Check**.

Configuration directory on Windows:

```text
C:\ProgramData\Datadog\conf.d\
```

The process check configuration is:

```text
C:\ProgramData\Datadog\conf.d\process.d\conf.yaml
```

The Process check is included with the Agent but needs configuration for the processes you want to monitor. ([Datadog Monitoring][2])

Example:

```yaml
init_config:

instances:
  - name: my_application
    search_string:
      - myapp.exe
```

Then restart the Agent:

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" restart-service
```

---

# 4. What Can You Monitor?

The Process check can collect resource information for matching processes, including:

* CPU
* Memory
* I/O
* Number of threads

It can also be used with a **Process Check Monitor** to alert when the expected number of matching processes is not running. ([Datadog Monitoring][2])

Example:

```text
Expected:
myapp.exe = 1 process

Actual:
myapp.exe = 0 processes

        ↓

Datadog Monitor
        ↓
ALERT
```

---

## 5. Troubleshooting

If processes aren't appearing:

```text
1. Check Datadog Agent service
          ↓
2. Check process configuration
          ↓
3. Check Agent status
          ↓
4. Restart Agent
          ↓
5. Check agent.log
```

Agent log:

```text
C:\ProgramData\Datadog\logs\agent.log
```

One Windows-specific consideration is **Agent permissions**. Depending on how the Agent runs, it may not have access to complete command-line/user information for processes running under other users. ([Datadog Monitoring][3])

### Interview Point

> **Live Process Monitoring** gives real-time visibility into processes, while the **Process Check** is useful when you want to specifically monitor selected processes and create alerts based on their status/count.

[1]: https://docs.datadoghq.com/infrastructure/process/?utm_source=chatgpt.com "Live Processes"
[2]: https://docs.datadoghq.com/integrations/process/?utm_source=chatgpt.com "Processes"
[3]: https://docs.datadoghq.com/agent/guide/windows-agent-ddagent-user/?utm_source=chatgpt.com "Datadog Windows Agent User"

# Datadog Linux Agent Setup

The **Datadog Agent** runs on a Linux host and collects system metrics, logs, traces, and integration data, then sends them to Datadog.

## 1. Prerequisites

Before installation, ensure:

* Linux server
* Datadog account
* Datadog API Key
* `sudo` access
* Internet connectivity to Datadog

Official documentation: [Datadog Linux Agent Installation](https://docs.datadoghq.com/agent/basic_agent_usage/linux/?utm_source=chatgpt.com)

---

## 2. Install the Agent

For Debian/Ubuntu-based systems, Datadog provides an installation command through the Agent installation page.

A typical installation uses:

```bash
DD_API_KEY="<YOUR_API_KEY>" \
DD_SITE="datadoghq.com" \
bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script_agent7.sh)"
```

> Use your actual Datadog site if your organization uses a different Datadog region.

---

## 3. Check Agent Status

After installation:

```bash
sudo systemctl status datadog-agent
```

You should see:

```text
Active: active (running)
```

You can also run:

```bash
sudo datadog-agent status
```

This provides detailed information about the Agent and enabled checks.

---

## 4. Start / Stop / Restart Agent

### Start

```bash
sudo systemctl start datadog-agent
```

### Stop

```bash
sudo systemctl stop datadog-agent
```

### Restart

```bash
sudo systemctl restart datadog-agent
```

### Enable at boot

```bash
sudo systemctl enable datadog-agent
```

---

## 5. Main Configuration File

The primary Agent configuration file is:

```text
/etc/datadog-agent/datadog.yaml
```

Example:

```yaml
api_key: <YOUR_API_KEY>
site: datadoghq.com
```

After configuration changes:

```bash
sudo systemctl restart datadog-agent
```

---

## 6. Check Host in Datadog

After the Agent starts successfully:

```text
Datadog
   ↓
Infrastructure
   ↓
Hosts
```

Your Linux server should appear as a host once the Agent successfully communicates with Datadog.

You can then monitor:

* CPU
* Memory
* Disk
* Network
* Load
* Processes
* System metrics
* Agent status

---

## 7. Agent Logs

Default Agent log location:

```text
/var/log/datadog/agent.log
```

Check recent logs:

```bash
sudo tail -f /var/log/datadog/agent.log
```

Useful when troubleshooting:

```text
Agent not starting
API authentication issue
Network/connectivity issue
Integration failure
Configuration error
```

---

## 8. Linux Agent Troubleshooting Flow

```text
Linux Server
     ↓
Install Datadog Agent
     ↓
Check systemctl status
     ↓
Check datadog-agent status
     ↓
Verify API Key + Datadog Site
     ↓
Check Network / Proxy
     ↓
Check agent.log
     ↓
Infrastructure → Hosts
```

### Interview Quick Revision

| Item           | Linux                                  |
| -------------- | -------------------------------------- |
| Agent service  | `datadog-agent`                        |
| Main config    | `/etc/datadog-agent/datadog.yaml`      |
| Logs           | `/var/log/datadog/agent.log`           |
| Status         | `sudo datadog-agent status`            |
| Service status | `sudo systemctl status datadog-agent`  |
| Restart        | `sudo systemctl restart datadog-agent` |
| Enable at boot | `sudo systemctl enable datadog-agent`  |

**Key point:**
`datadog-agent status` is your first useful command after installation because it helps verify the Agent, configuration, and integrations before troubleshooting further.

Yes. For your **Datadog notes**, this is an important topic because Agent-level tags are one of the main ways to organize and filter hosts.

# Datadog — Agent-Level Tags

## 1. What are Agent-Level Tags?

**Agent-level tags** are tags configured in the Datadog Agent's main configuration file. They are applied to telemetry sent by that Agent, including metrics, events, logs, traces, and service checks. ([Datadog Monitoring][1])

Common examples:

```text
env:production
team:infrastructure
app:web
region:hyderabad
role:webserver
```

The recommended format is:

```text
<key>:<value>
```

For example:

```text
env:production
```

---

# 2. Where to Configure Tags?

### Windows

Main configuration file:

```text
C:\ProgramData\Datadog\datadog.yaml
```

Datadog documents this as the main Windows Agent configuration file. ([Datadog Monitoring][2])

### Linux

```text
/etc/datadog-agent/datadog.yaml
```

---

# 3. Configure Agent-Level Tags

Open `datadog.yaml`.

### Windows example

```yaml
tags:
  - env:production
  - team:infrastructure
  - app:web
  - role:webserver
```

### Linux example

```yaml
tags:
  - env:production
  - team:infrastructure
  - app:web
  - role:webserver
```

Datadog supports the `tags` parameter as a list of key-value tags. ([Datadog Monitoring][3])

---

# 4. Restart the Agent

After modifying the configuration, restart the Agent.

### Windows

```powershell
& "$env:ProgramFiles\Datadog\Datadog Agent\bin\agent.exe" restart-service
```

### Linux

```bash
sudo systemctl restart datadog-agent
```

Configuration changes require an Agent restart to take effect. ([Datadog Monitoring][2])

---

# 5. How to Verify the Tags?

After the Agent starts sending data, go to:

```text
Datadog
   ↓
Infrastructure
   ↓
Hosts
```

Find your host and open its details.

The host's tags can be viewed in the host details, and the Host List can also display tags as columns. ([Datadog Monitoring][4])

You can also verify tags through a metric.

Go to:

```text
Metrics
   ↓
Summary
```

Search for:

```text
datadog.agent.started
```

Open the metric and inspect its tags.

You should see something like:

```text
host:my-windows-server
env:production
team:infrastructure
app:web
role:webserver
```

Datadog specifically documents `datadog.agent.started` as a useful metric for confirming Agent data and tags. ([Datadog Monitoring][1])

---

# 6. How to Use Tags for Filtering?

This is where tags become very useful.

Suppose you have:

```text
Server 1 → env:production
Server 2 → env:production
Server 3 → env:testing
Server 4 → env:development
```

In:

```text
Infrastructure → Hosts
```

you can filter using:

```text
env:production
```

Now you see only the production hosts.

Datadog supports tag filtering and grouping in the Infrastructure List, Host Map, Processes, Containers, and other areas. ([Datadog Monitoring][5])

---

# 7. Group Hosts by Tags

Suppose you have:

```text
env:production
env:testing
env:development
```

You can use the **Group by** option to group hosts according to a tag key such as:

```text
env
```

Result conceptually:

```text
Production
 ├── server-01
 ├── server-02
 └── server-03

Testing
 ├── server-04
 └── server-05

Development
 └── server-06
```

---

# 8. Using Tags in Metrics

Suppose you have a CPU metric:

```text
system.cpu.user
```

You can filter it using:

```text
env:production
```

Or group it by:

```text
host
```

or:

```text
env
```

For example:

```text
system.cpu.user{env:production}
```

This lets you analyze CPU usage specifically for production hosts.

Tags are designed to allow Datadog telemetry to be **filtered, aggregated, and compared**. ([Datadog Monitoring][6])

---

# 9. Using Tags in Monitors

Tags are particularly useful when creating monitors.

For example, instead of creating separate CPU monitors for every production server, you can scope a monitor to:

```text
env:production
```

A host monitor can include or exclude hosts using tags. ([Datadog Monitoring][7])

Conceptually:

```text
CPU > 80%
       +
env:production
       ↓
Alert
```

So the monitor applies to the relevant production hosts rather than every host.

---

# 10. Practical Example

Imagine your Windows infrastructure contains:

```text
WEB01
WEB02
DB01
DB02
```

Configure:

### WEB01

```yaml
tags:
  - env:production
  - role:webserver
  - team:application
```

### WEB02

```yaml
tags:
  - env:production
  - role:webserver
  - team:application
```

### DB01

```yaml
tags:
  - env:production
  - role:database
  - team:database
```

### DB02

```yaml
tags:
  - env:production
  - role:database
  - team:database
```

Now you can filter:

```text
env:production
```

→ All production servers

```text
role:webserver
```

→ WEB servers

```text
role:database
```

→ Database servers

```text
team:application
```

→ Application team's servers

---

## 11. Simple Architecture

```text
             Windows / Linux Host
                     |
                     ↓
              Datadog Agent
                     |
              datadog.yaml
                     |
          ┌──────────┴──────────┐
          ↓                     ↓
    Metrics / Logs         Host Metadata
          |                     |
          └──────────┬──────────┘
                     ↓
                  Datadog
                     |
          ┌──────────┼───────────┐
          ↓          ↓           ↓
       Hosts      Metrics     Monitors
          |
       Filtering
          |
     env:production
```

### Interview Quick Revision

**Q: Where do you configure Agent-level tags?**

Windows:

```text
C:\ProgramData\Datadog\datadog.yaml
```

Linux:

```text
/etc/datadog-agent/datadog.yaml
```

**Q: Example?**

```yaml
tags:
  - env:production
  - team:infra
  - role:webserver
```

**Q: Why use tags?**

> To **filter, group, aggregate, and scope** Datadog telemetry and infrastructure.

**Q: Where can you use them?**

> Infrastructure, Metrics, Dashboards, Monitors, Events, Logs, APM, and other Datadog products. ([Datadog Monitoring][6])

**Key concept:**
**Configure once at Agent level → telemetry inherits the tags → use those tags throughout Datadog for filtering, grouping, dashboards, and monitoring.** ([Datadog Monitoring][1])

[1]: https://docs.datadoghq.com/getting_started/agent/?utm_source=chatgpt.com "Getting Started with the Agent"
[2]: https://docs.datadoghq.com/agent/supported_platforms/windows/?utm_source=chatgpt.com "Windows"
[3]: https://docs.datadoghq.com/getting_started/tagging/assigning_tags/?utm_source=chatgpt.com "Assigning Tags"
[4]: https://docs.datadoghq.com/infrastructure/list/?utm_source=chatgpt.com "Host List"
[5]: https://docs.datadoghq.com/getting_started/tagging/using_tags/?utm_source=chatgpt.com "Using Tags"
[6]: https://docs.datadoghq.com/getting_started/tagging/?utm_source=chatgpt.com "Getting Started with Tags"
[7]: https://docs.datadoghq.com/monitors/types/host/?utm_source=chatgpt.com "Host Monitor"

# Datadog — Enable Process Monitoring on Linux

Datadog provides **Live Processes** to monitor processes running on a Linux host. The **Process Agent** collects process-level information and sends it to Datadog.

## 1. Edit `datadog.yaml`

Open:

```bash
sudo vi /etc/datadog-agent/datadog.yaml
```

Enable process collection:

```yaml
process_config:
  process_collection:
    enabled: true
```

Save the file.

---

## 2. Restart Datadog Agent

```bash
sudo systemctl restart datadog-agent
```

Check the service:

```bash
sudo systemctl status datadog-agent
```

You should see:

```text
Active: active (running)
```

---

## 3. Verify Process Agent

Run:

```bash
sudo datadog-agent status
```

Look for the **Process Agent** section and verify that process collection is running.

You can also check the Agent log:

```bash
sudo tail -f /var/log/datadog/agent.log
```

---

## 4. View Processes in Datadog

Once data is being received:

```text
Datadog
   ↓
Infrastructure
   ↓
Processes
```

You can investigate processes by:

* Host
* Process name
* CPU usage
* Memory usage
* Process state
* Command
* Tags

---

## 5. Example

Suppose your Linux server is running:

```text
nginx
sshd
java
docker
```

After enabling Process Monitoring, you can use Datadog to investigate these processes and their resource consumption.

Conceptually:

```text
Linux Host
    ↓
Datadog Agent
    ↓
Process Agent
    ↓
Process Information
    ↓
Datadog
    ↓
Infrastructure → Processes
```

### Interview Point

> **Process Monitoring provides process-level visibility that is more detailed than host-level CPU and memory monitoring.** It helps identify which processes are consuming resources on a host.

### Troubleshooting

If processes aren't visible:

```text
1. Check Agent service
       ↓
2. Check datadog-agent status
       ↓
3. Verify process_collection.enabled
       ↓
4. Restart Agent
       ↓
5. Check /var/log/datadog/agent.log
       ↓
6. Check Datadog → Infrastructure → Processes
```

[Datadog — Live Processes](https://docs.datadoghq.com/infrastructure/process/?utm_source=chatgpt.com)

Absolutely. Below is a **GitHub-ready Datadog notes section** covering Synthetic tests, Metric/Host monitors, Composite monitors, Downtime, and AWS/Azure integrations.

# Datadog — Synthetic Tests, Monitors & Cloud Integrations

## 1. Synthetic API Test

### What is a Synthetic API Test?

A Synthetic API test periodically sends requests to an API endpoint and verifies things such as:

* HTTP status code
* Response time
* Response headers
* Response body
* API availability

Datadog supports HTTP, SSL, DNS, WebSocket, TCP, UDP, ICMP and gRPC API tests. ([Datadog Monitoring][1])

### How to Create

**Path:**

`Digital Experience → Tests → New Test → API Test`

For an HTTP API:

1. Select **HTTP**.
2. Enter the API URL.
3. Select HTTP method:

   * GET
   * POST
   * PUT
   * PATCH
   * DELETE
4. Add authentication/headers/body if required.
5. Click **Send** to test the request.
6. Configure assertions.

Example:

```text
URL:
https://api.example.com/health

Method:
GET

Expected Status:
200

Response Time:
< 2000 ms
```

7. Select **locations** from which Datadog should execute the test.
8. Configure frequency.
9. Add tags such as:

```text
env:production
service:payment-api
team:backend
```

10. Configure notification/alert message.
11. Click **Create Test / Save**.

Datadog automatically associates a Synthetic monitor with the Synthetic test. ([Datadog Monitoring][1])

### Where to See It?

`Digital Experience → Tests`

You can search/filter your Synthetic tests there.

The associated monitor can also be found under:

`Monitors → Manage Monitors`

For Synthetic monitors, search:

```text
type:synthetics
```

([Datadog Monitoring][2])

---

# 2. Synthetic Browser Test

### What is a Browser Test?

A Browser Synthetic test simulates a real user's browser journey.

Example:

```text
Open Website
     ↓
Login
     ↓
Search Product
     ↓
Add to Cart
     ↓
Checkout
```

Datadog executes these steps periodically from selected browsers/devices/locations. ([Datadog Monitoring][3])

### How to Create

**Path:**

`Digital Experience → Tests → New Test → Browser Test`

### Step-by-Step

1. Select **Browser Test**.
2. Enter **Starting URL**.
3. Enter a test name.

Example:

```text
Name:
Website Login Journey

URL:
https://example.com
```

4. Add environment and tags:

```text
env:production
app:web
team:frontend
```

5. Select:

   * Browser
   * Device
   * Managed/Private Location
   * Test frequency

6. Click:

`Save & Edit Recording`

7. Install the **Datadog Test Recorder** browser extension if required.
8. Click **Start Recording**.
9. Perform the user journey.

For example:

```text
Open login page
        ↓
Enter username
        ↓
Enter password
        ↓
Click Login
        ↓
Verify Dashboard
```

10. Add assertions.

Example:

```text
Current URL contains:
dashboard

Page contains:
Welcome
```

11. Click **Save and Launch Test**. ([Datadog Monitoring][4])

### Where to See It?

`Digital Experience → Tests`

You can also find the generated Synthetic monitor through:

`Monitors → Manage Monitors`

Filter:

```text
type:synthetics
```

([Datadog Monitoring][2])

---

# 3. Metric Monitor / Metric Alert

### What is a Metric Monitor?

A Metric Monitor watches a metric and triggers an alert when the metric crosses a configured threshold.

Example:

```text
CPU > 80%
```

or

```text
Disk Usage > 90%
```

Datadog allows any metric reporting to Datadog to be used in a metric monitor. ([Datadog Monitoring][5])

### Create a Metric Alert

**Path:**

`Monitors → New Monitor → Metric`

### Example — CPU Alert

Select metric:

```text
system.cpu.user
```

Filter:

```text
env:production
```

Group by:

```text
host
```

Set evaluation:

```text
Average over last 5 minutes
```

Condition:

```text
> 80
```

Example logic:

```text
system.cpu.user
        ↓
env:production
        ↓
Average
        ↓
Last 5 minutes
        ↓
> 80%
        ↓
ALERT
```

Datadog's metric monitor configuration includes the metric, filters, aggregation, grouping and evaluation window. ([Datadog Monitoring][5])

---

# 4. Metric Alert → Send Email

After configuring the alert condition, go to the **message/notification** section.

Example:

```text
CPU usage is above 80% on {{host.name}}

@your-email@example.com
```

The `@` mention is used to notify the selected notification target.

You can also use notification integrations such as:

```text
Email
Slack
PagerDuty
Microsoft Teams
```

Then click:

`Save / Create Monitor`

Datadog monitor messages support notification targets and can include monitor variables/details. ([Datadog Monitoring][6])

### Simple Example

```text
Monitor:
Production CPU Alert

Condition:
CPU > 80%

Notification:
@team@example.com
```

---

# 5. Host Monitor Setup

### What is a Host Monitor?

A Host Monitor checks whether a host is still reporting data to Datadog.

The Agent reports the service check:

```text
datadog.agent.up
```

A Host Monitor can alert when the host stops reporting for the configured period. ([Datadog Monitoring][7])

### Create Host Monitor

**Path:**

`Monitors → New Monitor → Host`

### Select Hosts

You can monitor:

```text
Specific Host
```

or

```text
Host Tags
```

or

```text
All Monitored Hosts
```

Example:

```text
env:production
```

This monitors production hosts.

You can also exclude hosts using tags. ([Datadog Monitoring][7])

### Alert Condition

Example:

```text
Host stops reporting
        ↓
More than 2 minutes
        ↓
ALERT
```

Datadog provides both:

* **Check Alert**
* **Cluster Alert**

Cluster Alert can alert when a percentage of hosts stop reporting. ([Datadog Monitoring][7])

---

# 6. Where to See List of Monitors?

**Path:**

`Monitors → Manage Monitors`

This is the central place to search and manage monitors.

You can filter/search based on things such as:

```text
Monitor name
Tags
Status
Monitor type
Team
```

Examples:

```text
type:metric
```

```text
type:host
```

```text
type:synthetics
```

For Synthetic monitors specifically, Datadog documents `type:synthetics` as a Manage Monitors filter. ([Datadog Monitoring][2])

### Common Monitor Types

```text
Metric
Host
Composite
Log
APM
Process
Network
SLO
Synthetic
Integration
```

([Datadog Monitoring][6])

---

# 7. Composite Monitor

### What is a Composite Monitor?

A Composite Monitor combines multiple existing monitors using Boolean logic.

Example:

```text
Monitor A = CPU > 80%
Monitor B = Memory > 90%

Composite:
A && B
```

The composite alerts only when **both conditions are true**. ([Datadog Monitoring][8])

### Create Composite Monitor

**Path:**

`Monitors → New Monitor → Composite`

Select existing monitors.

Example:

```text
A = CPU High
B = Memory High
```

Set:

```text
A && B
```

Other examples:

```text
A || B
```

```text
A && !B
```

Datadog currently allows up to **10 individual monitors** in a composite monitor, and a composite cannot be based on another composite monitor. ([Datadog Monitoring][8])

### Practical Example

```text
CPU High
   +
Memory High
   ↓
Composite Monitor
   ↓
Send Email
```

This can reduce alerts when only one symptom occurs.

---

# 8. Scheduled Downtime

### What is Downtime?

Downtime temporarily **silences monitor notifications** during planned activities such as:

* Server maintenance
* Application deployment
* OS patching
* Database maintenance
* Infrastructure upgrades

Downtime suppresses alerts/notifications but does **not stop the monitor from evaluating or changing state**. ([Datadog Monitoring][9])

### Create Scheduled Downtime

**Path:**

`Monitors → Manage Downtime`

Then:

`Schedule Downtime`

### Select What to Silence

You can target:

```text
Specific Monitor
```

or

```text
Monitor Tags
```

or

```text
Group Scope
```

Example:

```text
env:production
```

You can preview affected monitors before scheduling the downtime. ([Datadog Monitoring][9])

### One-Time Downtime

Example:

```text
Start:
22:00

End:
23:00

Reason:
Production server maintenance
```

### Recurring Downtime

Example:

```text
Every Sunday
02:00 – 04:00
```

Useful for regular maintenance windows. ([Datadog Monitoring][9])

---

# 9. AWS Integration — Manual Setup

### Purpose

AWS Integration allows Datadog to collect AWS data such as:

```text
EC2
S3
RDS
Lambda
ELB
CloudFront
ECS
EKS
CloudWatch metrics
```

### Manual Setup

**Datadog:**

`Integrations → AWS → Add AWS Account → Manually`

For AWS commercial accounts, the current manual role-delegation setup uses an IAM role and an External ID. ([Datadog Monitoring][10])

### High-Level Flow

```text
Datadog
   ↓
Generate External ID
   ↓
AWS IAM
   ↓
Create IAM Role
   ↓
Trust Datadog Account
   ↓
Add External ID
   ↓
Attach Required Permissions
   ↓
Return to Datadog
   ↓
Enter AWS Account ID + Role Name
   ↓
Save
```

### AWS Side

1. Open AWS Console.
2. Go to:

`IAM → Roles → Create Role`

3. Configure the trusted entity for Datadog.
4. Require the generated **External ID**.
5. Attach the required permissions/policies.
6. Create the role.

### Back in Datadog

Enter:

```text
AWS Account ID
AWS Role Name
```

Then click **Save**.

Datadog validates the role by attempting to assume it. Data can take several minutes to begin appearing after successful setup. ([Datadog Monitoring][10])

### Where to See AWS Data?

Typically:

`Infrastructure → AWS`

and AWS-specific dashboards/metrics.

---

# 10. Azure Integration — Manual Setup

### Purpose

Azure Integration allows Datadog to collect Azure metrics, logs and configuration information from Azure resources. ([Datadog Monitoring][11])

### High-Level Architecture

```text
Azure Subscription
       ↓
Microsoft Entra ID
       ↓
App Registration
       ↓
Monitoring Permissions
       ↓
Datadog Azure Integration
       ↓
Azure Metrics / Logs / Configuration
```

### Manual Setup

**Datadog:**

`Integrations → Azure`

Choose the Azure integration setup.

For an app-registration-based setup, configure an Azure application/service principal and grant it access to the subscriptions/management groups you want Datadog to monitor. ([Datadog Monitoring][12])

### Basic Flow

1. Open **Azure Portal**.
2. Go to:

`Microsoft Entra ID → App registrations`

3. Create/select an App Registration.
4. Note:

```text
Tenant ID
Client ID
```

5. Configure the required Azure permissions.
6. Assign the required monitoring access to the target subscriptions.
7. In Datadog:

`Integrations → Azure → Add Existing`

8. Enter the required tenant/client credentials.
9. Configure subscriptions/resource collection.
10. Click **Create Configuration**.

Datadog currently supports **Secretless Auth** using federated credentials as well as **Client Secret** authentication; Secretless Auth is the recommended method on supported sites. ([Datadog Monitoring][12])

### Where to See Azure Data?

```text
Infrastructure
     ↓
Azure resources

Metrics
     ↓
Metrics → Summary
```

You can search Azure metrics from **Metrics → Summary**. ([Datadog Monitoring][13])

---

# Quick Interview Revision

| Topic             | Datadog Path                                           |
| ----------------- | ------------------------------------------------------ |
| Synthetic API     | `Digital Experience → Tests → New Test → API Test`     |
| Synthetic Browser | `Digital Experience → Tests → New Test → Browser Test` |
| Metric Monitor    | `Monitors → New Monitor → Metric`                      |
| Host Monitor      | `Monitors → New Monitor → Host`                        |
| Composite         | `Monitors → New Monitor → Composite`                   |
| Monitor List      | `Monitors → Manage Monitors`                           |
| Downtime          | `Monitors → Manage Downtime`                           |
| AWS               | `Integrations → AWS`                                   |
| Azure             | `Integrations → Azure`                                 |

### Important Concepts

```text
Synthetic Test
     ↓
Automatically associated Synthetic Monitor
     ↓
Failure
     ↓
Notification
```

```text
Metric
  ↓
Metric Monitor
  ↓
Threshold
  ↓
Alert
  ↓
Email / Slack / PagerDuty
```

```text
Monitor A + Monitor B
        ↓
Composite Monitor
        ↓
Boolean condition
        ↓
Alert
```

```text
AWS / Azure
    ↓
Cloud Integration
    ↓
Cloud Metrics
    ↓
Datadog
    ↓
Dashboard / Monitor / Alert
```

[Datadog Synthetic Monitoring documentation](https://docs.datadoghq.com/synthetics/?utm_source=chatgpt.com)
[Datadog Monitors documentation](https://docs.datadoghq.com/monitors/?utm_source=chatgpt.com)
[Datadog AWS integration documentation](https://docs.datadoghq.com/integrations/amazon-web-services/?utm_source=chatgpt.com)
[Datadog Azure integration documentation](https://docs.datadoghq.com/integrations/azure/?utm_source=chatgpt.com)

[1]: https://docs.datadoghq.com/getting_started/synthetics/api_test/?utm_source=chatgpt.com "Getting Started with API Tests"
[2]: https://docs.datadoghq.com/monitors/types/synthetic_monitoring/?utm_source=chatgpt.com "Synthetic Monitors"
[3]: https://docs.datadoghq.com/synthetics/browser_tests/?utm_source=chatgpt.com "Browser Testing"
[4]: https://docs.datadoghq.com/getting_started/synthetics/browser_test/?utm_source=chatgpt.com "Getting Started with Browser Tests"
[5]: https://docs.datadoghq.com/monitors/types/metric/?utm_source=chatgpt.com "Metric Monitor"
[6]: https://docs.datadoghq.com/api/latest/monitors/create-a-monitor/?utm_source=chatgpt.com "Create a monitor"
[7]: https://docs.datadoghq.com/monitors/types/host/?utm_source=chatgpt.com "Host Monitor"
[8]: https://docs.datadoghq.com/monitors/types/composite/?utm_source=chatgpt.com "Composite Monitor"
[9]: https://docs.datadoghq.com/monitors/downtimes/?utm_source=chatgpt.com "Downtimes"
[10]: https://docs.datadoghq.com/integrations/guide/aws-manual-setup/?utm_source=chatgpt.com "AWS Manual Setup Guide"
[11]: https://docs.datadoghq.com/integrations/guide/azure-integrations/?utm_source=chatgpt.com "Azure Integrations"
[12]: https://docs.datadoghq.com/getting_started/integrations/azure/?utm_source=chatgpt.com "Getting Started with Azure"
[13]: https://docs.datadoghq.com/getting_started/integrations/azure/?tab=createanappregistration&utm_source=chatgpt.com "Getting Started with Azure"
