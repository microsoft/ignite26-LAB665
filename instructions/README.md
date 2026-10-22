# LAB665: See how far one agent goes in Copilot Studio

These instructions are for participants in the instructor-led Microsoft Ignite 2026 lab **LAB665: See how far one agent goes in Copilot Studio**.

## Lab overview

In this 60-minute hands-on lab, you will build a Supplier Assurance Agent for Caldova Pharmaceuticals. The agent reviews a supplier invoice, checks current operational records through SharePoint connector tools or the SharePoint MCP, grounds its decisions in contracts and approvals stored in SharePoint, runs Python in the GitHub Copilot harness sandbox, creates a PDF review brief, records a nonfinancial review log, and participates in a workflow.

The agent recommends what Caldova can process and what it should challenge. It never pays an invoice, rejects a charge, changes supplier status, or replaces an authorized reviewer.

## Skillable conventions

Text surrounded by `+++` becomes clickable autotype text in Skillable. Variables such as `@lab.CloudCredential(...)` and `@lab.Variable(...)` resolve when the hosted lab runs.

This lab currently uses the shared Skillable credential ID `AITour27M365E7`. Keep that ID when configuring the hosted lab resources.

> [!IMPORTANT]
> Wait for autotype to finish before clicking elsewhere in the virtual machine. At home, replace Skillable variables with values from your own environment.

## What you will build

- A Copilot Studio agent with focused instructions and guardrails
- SharePoint knowledge grounded in contracts, policies, approvals, and quality documents
- SharePoint connector tools or an MCP connection for live list reads and a controlled review-log write
- An Invoice Fact Check skill created in the authoring experience
- An uploaded Invoice Review Decision skill with packaged Python
- A reusable Agent Ops evaluation
- A simple three-node workflow built from scratch with your published agent

## Lab sections

1. [Introduction and sign in](./00-Introduction.md)
2. [Build the Supplier Assurance Agent](./01-Build-The-Agent.md)
3. [Add SharePoint knowledge](./02-Add-SharePoint-Knowledge.md)
4. [Add the SharePoint connector](./03-Connect-SharePoint.md) (recommended alternative), or [connect the SharePoint MCP](./03-Connect-SharePoint-MCP.md)
5. [Add skills and review an invoice](./04-Add-Skills-And-Review-Invoice.md)
6. [Evaluate and publish the agent](./05-Evaluate-And-Publish.md)
7. [Build the workflow](./06-Create-The-Workflow.md)
8. [Run the solution end to end](./07-Test-End-To-End.md)

For section 3, complete only one path. Use the connector path when the SharePoint MCP is unavailable or unreliable; both paths continue to section 4.

## Lab files

The Skillable virtual machine provides the files under:

```text
D:\LabFiles
```

The SharePoint site, reference documents, operational lists, learner account, mailbox, and Power Platform environment are prepared before the session.

Select **Next** to begin.
