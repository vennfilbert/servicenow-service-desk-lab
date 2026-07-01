# servicenow-service-desk-lab
ITIL-aligned service desk lab: incident and service request handling in ServiceNow, with a documented knowledge base.

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