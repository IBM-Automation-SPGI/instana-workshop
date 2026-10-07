# **Lab 0 — Environment, Console, and Dynamic Focus**

<span class="lab-badge">LAB 0</span><span class="lab-time">⏱ 15 minutes</span>

---

## **1. Theoretical Foundations of Modern Observability**

The shift from monolithic applications toward distributed microservice architectures, ephemeral containers, and hybrid clouds has fundamentally transformed monitoring. In a dynamic environment, the three classic pillars of observability (Metrics, Logs, and Traces) are insufficient when analyzed in disconnected silos.

**IBM Instana** introduces a paradigm centered on **Continuous, Automated Observability**, built on four essential capabilities:

1. **Continuous Auto-Discovery:** Passive and active discovery of physical, logical, and network components without human intervention.
2. **Dynamic Graph:** An in-memory temporal graph maintaining live dependencies between infrastructure and application code.
3. **High-Fidelity Metrics (1-Second Resolution):** Instant capture of CPU and memory micro-bursts that traditional 1-to-5 minute averages hide.
4. **100% Tracing No-Sampling:** Every single transaction is recorded and contextualized for auditing and troubleshooting without data loss.

In this foundational lab, you will explore the hands-on environment (**IBM Dev Sandbox**), learn to navigate the user interface, master time controls, and leverage the universal search engine: **Dynamic Focus**.

---

## **2. Accessing the Instana Dev Sandbox Console**

1. Open your web browser and navigate to:
   [:octicons-link-external-24: https://ibmdevsandbox-instanaibm.instana.io/#/home](https://ibmdevsandbox-instanaibm.instana.io/#/home)
2. Sign in using the corporate identity provider (SSO).
3. After authentication, you will access the **Home Overview** dashboard:

<div class="screenshot-container">
  <img src="../assets/screenshots/lab0_home.png" alt="Instana Sandbox Home Overview" />
  <div class="screenshot-caption">Figure 0.1: Home Overview dashboard in IBM Instana Sandbox showing active incidents and quick access shortcuts.</div>
</div>

On this initial landing page, you will notice:

* **Updates & Community Banner:** Direct links to GraphQL APIs, official product documentation, and release notes.
* **Active Incidents Summary:** Real-time overview of correlated anomalies across environment clusters (e.g., service call spikes, database status alerts).
* **Agent Installation Shortcut:** The `Install agents or collectors` button provides ready-to-run installation scripts for Linux, Windows, macOS, Kubernetes, OpenShift, and public cloud providers (AWS, Azure, GCP, IBM Cloud).

---

## **3. Sidebar Navigation and Architecture**

The Instana console organizes its core capabilities in a high-contrast left sidebar:

| Icon / Module | Purpose and Core Capabilities |
| :--- | :--- |
| **🏠 Home** | Executive summary, real-time open incidents, documentation, and GraphQL API shortcuts. |
| **🌐 Websites & mobile apps** | **Real User Monitoring (RUM)**. Monitors end-user frontend experiences on web browsers and mobile apps (iOS/Android), tracking *Core Web Vitals* (LCP, FID, CLS), render times, and JavaScript errors. |
| **💼 Business processes** | Business process observability (e.g., *Checkout to Delivery*, *Loan Application Approval*) correlating technical services with business KPIs. |
| **📱 Applications** | **Application Perspectives**. Logical groupings of services, APIs, and microservices with RED metrics (Rate, Errors, Duration) and dependency maps. |
| **🤖 Gen AI observability** | Specialized telemetry for **Large Language Models (LLMs)** inferences, watsonx agents, token consumption, embedding latencies, and operational costs. |
| **☁️ Platforms** | Native monitoring for orchestration platforms including **Kubernetes, Red Hat OpenShift, Cloud Foundry, VMware vSphere, and Serverless (AWS Lambda)**. |
| **🗄️ Infrastructure** | **Infrastructure 3D Map**. Physical and virtual visualization of hosts, virtual machines, middleware runtimes (JVMs, Node.js, Go, Python), and databases. |
| **📊 Custom dashboards** | Interactive custom dashboards with multi-dimensional widgets. |
| **📋 Logs** | Contextual log search linked directly to distributed traces and emitting containers (*Logs in Context*). |
| **⏱️ Synthetic monitoring** | Periodic synthetic probes (HTTP checks, browser user journey scripts) executed across global points of presence to validate SLAs. |
| **🔍 Analytics** | **Unbounded Analytics**. High-performance analytics engine for querying, filtering, and grouping billions of traces, calls, and infrastructure metrics without cardinality limits. |
| **🛡️ Vulnerabilities** | Static and runtime CVE vulnerability assessment on loaded libraries across monitored processes. |
| **⚠️ Events** | Consolidated log of anomalies, warnings, change events (Git deployments, restarts), and **AI-grouped Incidents**. |

---

## **4. The Time Window Selector (Time Picker)**

Located in the top-right corner, the Time Picker is a vital tool for forensic analysis:

```text
┌─────────────────────────────────┐  ┌──────────┐
│  Oct 07 - Last hour          ▼  │  │  Live ▶  │
└─────────────────────────────────┘  └──────────┘
```

### Time Navigation Modes:

1. **Live Mode (Real-Time):**
   * When `Live ▶` is active, charts update automatically every 1 to 5 seconds.
   * Ideal for Network Operations Centers (NOC/SRE) and monitoring during production rollouts or load tests.
2. **Preset Ranges:**
   * `Last 10 minutes`, `Last hour`, `Last 24 hours`, `Last 7 days`, `Last 30 days`.
3. **Time Shift & Compare:**
   * Superimposes current metrics over the same timeframe from the previous day or week to uncover seasonal deviations.
4. **Custom Window (Absolute Range):**
   * Locks an exact historical time range (e.g., `2026-10-07 13:15:00` to `2026-10-07 13:30:00`) for post-incident reviews without data sliding forward.

---

## **5. Mastering the Dynamic Focus Bar (Lucene Queries)**

The **Dynamic Focus Bar** at the top header transforms the entire Instana UI by applying cross-cutting filters that instantly affect infrastructure, services, traces, and alerts.

<div class="screenshot-container">
  <img src="../assets/screenshots/lab0_dynamic_focus.png" alt="Dynamic Focus Bar in Instana" />
  <div class="screenshot-caption">Figure 0.2: Universal Dynamic Focus search bar with contextual entity and tag auto-completion.</div>
</div>

### Query Syntax and Operators Table:

| Operator / Syntax | Usage Example | Description |
| :--- | :--- | :--- |
| **Exact match** | `entity.type:jvm` | Filters only Java Virtual Machine runtimes. |
| **Wildcard (`*`)** | `container.name:*catalogue*` | Matches any container name containing "catalogue". |
| **AND Operator** | `entity.zone:production AND entity.type:host` | Simultaneous zone and entity type match. |
| **OR Operator** | `call.http.status:500 OR call.http.status:502` | Matches either status code. |
| **NOT Operator** | `entity.type:host AND NOT entity.zone:test` | Excludes entities matching the condition. |
| **Numeric Comparison** | `call.duration:>200ms` | Filters calls with response times exceeding 200 ms. |
| **Numeric Range** | `call.http.status:[500 TO 599]` | Inclusive range matching 5xx HTTP server errors. |

### Hands-on Exercises with Dynamic Focus:

!!! example "Exercise 1: Filter by Database Technology"
    In the Dynamic Focus Bar, type the following query and press Enter:
    ```text
    entity.type:mongodb
    ```
    *Notice how the interface instantly isolates active MongoDB instances in the environment.*

!!! example "Exercise 2: Filter Application Containers"
    Clear the previous filter and enter:
    ```text
    container.name:*catalogue* OR container.name:*cart*
    ```
    *This isolates catalogue and shopping cart containers across the entire topology.*

!!! example "Exercise 3: Isolate Server Error Calls"
    Enter:
    ```text
    call.http.status:>=500
    ```
    *All telemetry focuses exclusively on transactions that generated critical 5xx server errors.*

---

## **6. Automation APIs: GraphQL and REST API**

Instana is built with an **API-First** architecture. Any metric or topology relationship visible in the GUI can be queried and automated through public APIs:

### Querying Topology with the GraphQL API
Instana exposes a GraphQL endpoint at `https://<instana-unit>/graphql` for querying the Dynamic Graph:

```graphql
query GetUnhealthyServices {
  application(id: "keda-scaler-robotapp") {
    name
    services {
      name
      health {
        status
        unresolvedIssuesCount
      }
      metrics {
        calls(window: "last-hour")
        erroneousCallRate(window: "last-hour")
        latency(window: "last-hour", aggregation: P95)
      }
    }
  }
}
```

---

## **7. Lab 0 Summary and Checklist**

Upon completing this lab, you have gained the skills to:

* :white_check_mark: Authenticate and sign in to the IBM Instana Dev Sandbox.
* :white_check_mark: Understand the role and scope of each sidebar navigation module.
* :white_check_mark: Master the *Time Picker*, switching between *Live* streams and historical forensic windows.
* :white_check_mark: Construct advanced *Dynamic Focus* queries to filter the observability scope.
* :white_check_mark: Explore automation opportunities using REST and GraphQL APIs.

---

[Continue to Lab 1: Infrastructure 3D, 1s Metrics & JVMs :octicons-arrow-right-24:](../lab1/index.md){ .md-button .md-button--primary }
