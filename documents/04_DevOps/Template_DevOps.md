
# DashBoard
## Development

### Deployment frequency(DF)
**Definition:** The frequency of successful releases to production to track delivery velocity.

0. Performance indicators:
* High frequency: Indicates small batch sizes, mature CI/CD pipelines, and high delivery throughput.
* Low frequency: Suggests large, risky batch sizes and potential bottlenecks in the release process.

1. Production deployment frequency dashboard
* **Source:** GitHub
* **Dashboard type:** Chart
* **Period:** Daily or weekly
* **Objective:** Displays the frequency of production CD workflow runs over time.

---

### Lead time for changes(LTFC)
**Definition:** The time it takes for a commit to reach production to identify delivery bottlenecks.

0. Performance indicators:
* High lead time (Low performance): Indicates inefficient processes, manual hurdles, or long feedback loops.
* Low lead time (High performance): Signifies efficient automation, fast code reviews, and rapid delivery.

1. Lead-time-for-change (PR creation to release note)
* **Source:** GitHub
* **Dashboard type:** Chart
* **Period:** Monthly
* **Objective:** Identifies delays in the development pipeline to shorten feedback loops and increase delivery velocity.

2. Lead-time-for-change (PR volume per release)
* **Source:** Github
* **Dashboard type:** Board
* **Period:** Per release version
* **Objective:** Optimizes release stability by managing batch size and reducing the risk associated with large deployments.


### Change failure rate(CFR)
**Definition:** The percentage of changes to production that result in degraded service and require immediate remediation.

0. Performance indicators:
* High rate (Low performance): Indicates unstable release quality, insufficient automated testing, or high manual error risks.
* Low rate (High performance): Signifies a robust QA process, effective automated testing, and a stable deployment environment.

1. Change failure rate monthly trend
* **Source**: GitHub (via Tag-based workflow)
* **Dashboard type:** Line / Bar Chart
* **Period:** Monthly
* **Objective**: Monitors the stability of releases over time. This metric acts as a "guardrail" to ensure that increasing delivery velocity (DF) does not compromise system stability. It helps identify if quality-focused initiatives, such as enhanced automated testing, are effectively reducing production risks.

2. CFR vs. Batch size correlation (PR count per release)

* **Source:** GitHub (via Tag-based workflow)
* **Dashboard type:** Scatter plot / Grouped Bar Chart
* **Period:** Per release version
* **Objective:** Visualizes the relationship between the number of Pull Requests included in a single release and the likelihood of failure.
* **Insight:** Identifies the team's "Safety Limit" for deployment size. By showing that releases with larger batch sizes have a higher probability of requiring hotfixes, this dashboard provides data-driven justification for moving toward smaller, more frequent, and lower-risk deployments.

### Time to restore service (TTRS)
**Definition:** The time it takes to recover from a failure in production.

0. Performance indicators:
* High time (Low performance): Suggests inadequate observability, slow incident response, or lack of automated recovery procedures.
* Low time (High performance): Indicates strong monitoring capabilities, clear incident protocols, and resilient system architecture.

1. Restoration time dashboard
* **Source:** Incident logs (based on failure simulations or actual failures)
* **Dashboard type:** Chart
* **Period:** Monthly
* **Objective:** Measures system resilience and the team's ability to minimize downtime during incidents.