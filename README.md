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
