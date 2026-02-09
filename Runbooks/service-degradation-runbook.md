# Incident Runbook – Service Degradation

**Service:** Example Application  
**Severity:** SEV-2 / SEV-3  
**Audience:** Operations / On-call Engineers  
**Last updated:** 2026-02-06  

---

## Purpose and Scope

This runbook describes the standard operational response to a service degradation incident.
It applies when the service is partially unavailable, responding slowly, or exhibiting reduced functionality,
but is not fully down.

The goal of this runbook is to:
- restore acceptable service performance as quickly as possible,
- minimize the user impact,
- provide a clear, repeatable response path for on-call engineers.

NOTE:
This runbook does not cover:
- complete service outage scenario (SEV-1),
- planned maintenance or deployments,
- incidents caused by confirmed external provider outages.

---

## Preconditions and Access Requirements

Before starting the investigation, make sure you have:

- access to application and infrastructure monitoring dashboards,
- access to centralized logging tools,
- read-only or operational access to the affected service,
- access to incident communication channels (e.g. Slack, Teams, email),
- access to the incident management or ticketing system.

If any required access is missing:
- escalate to the on-call lead or service owner,
- document the access gap in the incident timeline.
---

## Detection and Initial Assessment

Service degradation may be detected through:
- automated monitoring alerts (latency, error rate, resource usage),
- increase in user reports or customer support tickets,
- internal reports from engineering or operation teams.

**Initial assessment steps:**
1. Confirm whether the alert or report reflects a real user-facing impact.
2. Identify the affected service components and scope of impact.
3. Gather evidence (error messages, screenshots, steps to recreate the issue)
4. Determine the current severity level (typically SEV-2 or SEV-3).
5. Check for recent changes (deployments, configuration updates, infrastructure changes).

If the impact is unclear or expanding:
- treat the incident as potentially escalating,
- proceed with caution and ensure early communication.

---

## Immediate Actions (First 5–10 Minutes)

The first minutes of a service degradation incident are critical.
Focus on stabilizing the situation and establishing control, not on finding the root cause.

Perform the following actions in order:

1. Acknowledge the incident in the incident management system or alerting tool.
2. Verify the alert details and affected service components.
3. Check service health dashboards and key performance indicators.
4. Identify whether the issue is ongoing, intermittent, or already recovering.
5. Pause any ongoing deployments or configuration changes affecting the service.
6. Assign or confirm an incident owner.
7. Establish the technical communication channel (conference call, dedicated chat space, mailing group)
8. Start documenting actions and observations in the incident timeline.

**Do not:**
- make large-scale changes without understanding potential impact,
- restart services blindly unless explicitly covered by existing procedures,
- work on the incident alone without visibility from the team.

---

## Investigation and Mitigation Steps

Once the situation is stabilized, proceed with a structured investigation.
The goal is to identify the most likely cause of the degradation and apply safe, reversible mitigation actions.

### Investigation

Focus on recent changes and observable symptoms:

- Review monitoring data for anomalies (latency spikes, error rates, resource saturation).
- Analyze application and infrastructure logs for correlated errors or warnings.
- Check dependency health (databases, external APIs, message queues, caches).
- Review recent deployments, configuration changes, or infrastructure updates.
- Compare current system behavior with known healthy baselines.

If multiple potential causes are identified:
- prioritize hypotheses based on impact and likelihood,
- investigate **one change at a time** to avoid compounding effects.

### Mitigation

Apply mitigation actions that are:
- low-risk,
- reversible,
- well-understood by the team.

**Avoid applying multiple mitigation actions simultaneously, unless required to prevent further user impact.**

Common mitigation actions may include:
- rolling back a recent deployment or configuration change,
- temporarily disabling non-critical features,
- switching traffic from the primary resource to failover,
- scaling resources up or down to relieve pressure,
- restarting specific components only when supported by evidence or procedures.

After each mitigation action:
- observe system behavior and metrics,
- document the action and its effect,
- if the situation changes, reassess severity and user impact.

If mitigation attempts do not improve the situation:
- escalate to the service owner or senior engineering or platform support,
- consider invoking a higher severity response if user impact increases.

---

## Communication and Escalation
Clear and timely communication is critical during a service degradation incident.
The goal is to ensure shared situational awareness, coordinated action, and appropriate escalation.

### Internal Communication

Once the incident owner and technical communication channel are established:

- Provide a short incident summary (what is affected, current impact, known symptoms).
- Share updates in a regular cadence (e.g. every 20-30 minutes), even if there is no significant change.
- Clearly state assumptions, unknowns, and investigation steps, both taken and upcoming.
- Document key decisions and mitigation actions in the incident timeline.

Avoid speculation or assigning blame during the incident.
Focus on observable facts and current status.

### Stakeholder Communication

If the incident impacts users or business-critical functions:

- Notify relevant stakeholders according to the incident communication process.
- Use predefined communication channels or status pages where available.
- Use clear, non-technical language when communicating outside the engineering team.
- Provide realistic time estimates only when supported by evidence or confirmed by subject matter experts.
- Communicate uncertainty explicitly if timelines are unclear.

### Escalation

Escalate the incident when:

- mitigation actions do not improve the situation,
- the scope or user impact increases,
- the incident exceeds the current on-call team's expertise,
- service recovery timelines are uncertain.

Escalation may include:
- involving the service owner or system architect,
- engaging senior engineering or platform teams,
- increasing the incident severity level.

All escalations should be documented in the incident timeline.

---

## Resolution and Verification

Once mitigation actions have stabilized the service, confirm that the degradation is fully resolved.

Perform the following steps:

- Verify that key service metrics (latency, error rates, resource usage) have returned to acceptable baseline levels.
- Confirm service functionality through health checks, synthetic tests, or user validation where applicable.
- Ensure no new alerts related to the incident are firing.
- Monitor the service for a defined stabilization period to detect potential regressions.
- Confirm with relevant stakeholders that user impact has been mitigated.

**Do not close the incident until service stability is confirmed and no active mitigation is required.**

---

## Post-Incident Actions

Once the incident is resolved, perform the following actions:

- Update the incident ticket or record with a clear resolution summary.
- Ensure the incident timeline is complete and accurate.
- Identify whether a post-incident review or postmortem is required.
- Assign ownership for follow-up actions and remediation tasks.
- Capture lessons learned, including:
  - contributing factors,
  - detection gaps,
  - mitigation effectiveness,
  - communication effectiveness.

If a postmortem is conducted:
- focus on systemic improvements 
- avoid individual blame,
- document agreed action items with owners and timelines,
- track remediation work to completion.

---

## References
