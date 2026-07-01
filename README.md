# servicenow-service-desk-lab

A hands-on lab where I practised ITIL-aligned service desk work in ServiceNow: logging,
categorising, prioritising, resolving, and escalating incidents and service requests,
with a supporting knowledge base.

The lab was built in a ServiceNow Personal Developer Instance using the platform's
built-in sample data. The ticket scenarios (an account lockout, a VPN failure, a
site-wide outage, and so on) are practice scenarios I created to work through the full
ticket lifecycle end to end. The goal was to get genuinely comfortable with the tool
and the ITIL process, not to reproduce a real day's workload.

## What this demonstrates

- Handling the full incident lifecycle: log, categorise, set impact and urgency, assign,
  add work notes, resolve, and close.
- Triage judgement: setting impact and urgency correctly and letting the platform
  calculate priority, so similar-looking issues are ranked by real business effect.
- Knowing what to fix, what to gate, and what to escalate: resolving routine issues at
  L1, gating an access request on manager approval, and escalating both a stubborn
  incident and a major (P1) incident to the right team.
- Writing knowledge base articles for common tasks, the kind used for first-contact
  resolution.

## Tickets handled

Seven tickets built end to end (INC0010006 to INC0010012):

| Ticket | Issue | Type | Priority | Outcome |
| --- | --- | --- | --- | --- |
| INC0010006 | Account lockout | Incident | 3 - Moderate | Resolved at L1 |
| INC0010007 | Password reset | Request | 4 - Low | Resolved at L1 |
| INC0010008 | New starter onboarding | Request | 4 - Low | Fulfilled |
| INC0010009 | VPN will not connect | Incident | 3 - Moderate | Escalated to Network |
| INC0010010 | Outlook will not launch | Incident | 4 - Low | Resolved at L1 |
| INC0010011 | Shared drive access | Request | 4 - Low | Resolved after manager approval |
| INC0010012 | Site-wide shared drive outage | Incident | 1 - Critical | Major incident, escalated to Network |

Five handled at the service desk, two escalated (one standard, one major incident).

## Priority matrix (as observed in this instance)

Priority is calculated automatically from Impact and Urgency. These are the combinations
I exercised in this lab and the priority the instance produced for each:

| Impact | Urgency | Priority produced |
| --- | --- | --- |
| 1 - High | 1 - High | 1 - Critical |
| 3 - Low | 1 - High | 3 - Moderate |
| 3 - Low | 2 - Medium | 4 - Low |
| 3 - Low | 3 - Low | 4 - Low |

These are the values this instance returned for the tickets I built, rather than a
generic textbook matrix.

## Knowledge base

Six articles for common L1 tasks, in [servicenow-knowledge-base.md](servicenow-knowledge-base.md):
account lockout, password reset, VPN connection, Outlook profile repair, shared drive
access, and new starter onboarding. Each follows a consistent structure (symptom, cause,
resolution, verification, when to escalate) and describes a real, standard procedure.

## Build log
### Thursday 25 June 2026
- Signed up for the ServiceNow Developer Program and requested a Personal Developer Instance (Australia region). Request went into the queue; instance still provisioning due to high demand.
- Created the GitHub repository servicenow-service-desk-lab (public, with README) as the home for the project.
- Planned the build structure: 7 tickets to handle end to end (incidents and service requests), a priority matrix, and a knowledge base, all to be documented as an ITIL-aligned service desk lab.
- Extended the project deadline to next Sunday to allow the build to be done properly rather than rushed.


### Tuesday 30 June 2026
- ServiceNow PDI (dev412478, Australia release) finished provisioning and confirmed admin login.
- Learned the instance defaults new incidents to the Self Service view, which hides the analyst fields (Category, Impact, Assignment group, Priority). Switched the Incidents list to Default view to expose the full form.
- Handled Ticket 1 end to end: account lockout (INC0010006). Logged, categorised as Inquiry / Help, set Impact 3-Low and Urgency 1-High, which auto-calculated Priority 3-Moderate. Assigned to Service Desk, added work notes, and resolved with code "Solution provided".
- Noted this instance uses the resolution code "Solution provided" rather than "Solved (Permanently)".

### Tuesday 1 July 2026
- Handled tickets 2 through 7 end to end in ServiceNow, completing the full seven-ticket set (INC0010006 to INC0010012).
- Resolved four incidents at L1 with categorisation, impact and urgency, work notes, and resolution codes: account lockout, password reset, Outlook launch failure, and a shared drive access request (gated on manager approval).
- Fulfilled a new starter onboarding request covering account creation, security group membership, mailbox, licence, and shared drive access.
- Escalated a VPN connectivity incident to the Network team after L1 troubleshooting, left In Progress rather than resolved.
- Logged and escalated a Priority 1 major incident (site-wide shared drive outage) straight to Network, demonstrating major incident triage.
- Verified the instance calculates priority from impact and urgency, and documented the matrix as configured rather than assumed.
