# Integrations (Conceptual) — Jira Ops Lab

This lab demonstrates common enterprise integration patterns around Jira for IAM operations.

## 1) GitHub linkage (practical pattern)
**Goal:** Connect engineering work to Jira work items for traceability.

**Branch naming convention**
- feature/IOL-5-intake-form
- fix/IOL-12-approver-bug

**Commit message convention**
- IOL-5 Add required fields to access request intake
- IOL-12 Fix approver field population for Finance requests

**Pull request convention**
- PR title includes the Jira key (e.g., "IOL-5: Build access request intake form")
- PR description references acceptance criteria and links evidence

Result: Jira keys appear in Git history and PRs, enabling end-to-end traceability.


## 2) Slack / Teams notifications (conceptual pattern)
**Goal:** Reduce latency for approvals and SLA-sensitive requests.

**Event → Notification examples**
- When status changes to "Waiting for Approval" → notify #iam-approvals with ticket key + requester + due date
- When SLA due < 4 hours → notify #iam-oncall
- When ticket moves to Done → notify requester / channel with closure notes

**Suggested implementation options**
- Jira Automation rules (trigger: status change; action: send Slack/Teams message)
- Webhook → Function/Lambda → Teams/Slack webhook


## 3) ServiceNow handoff (conceptual pattern)
**Goal:** Support environments where ServiceNow is the ITSM system of record.

**Handoff rules**
- Jira is used for IAM team execution + reporting
- ServiceNow is used for enterprise request intake where required

**Field mapping**
- Jira field: External Ticket ID = ServiceNow RITM/INC number
- Jira status sync concept:
  - SNOW "In Progress" → Jira "Fulfillment"
  - SNOW "Closed" → Jira "Done"

**Closure**
- Jira is closed only after ServiceNow is closed and evidence is attached (audit readiness).
