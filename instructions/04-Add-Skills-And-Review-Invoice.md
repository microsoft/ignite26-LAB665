# 4 - Add Skills and Review an Invoice

The harness will coordinate two skills. Invoice Fact Check gathers and structures facts. Invoice Review Decision runs deterministic Python, applies the policy, and creates a PDF.

## Create Invoice Fact Check

1. Select the **Add** icon in the **Skills** section.

    ![Select the add button](./assets/04.1-add-skill-button.png)

1. Select the **Create from blank** tab.

    ![Select create from blank](./assets/04.2-create-from-blank.png)

1. Copy and paste `invoice-fact-check` in the **Name** input.

    ![Enter the skill name](./assets/04.3-skill-name.png)

1. Copy and paste the following in the **Description** input:

    ```text
    Use when a user asks to review a supplier invoice. Read the submitted invoice, retrieve current SharePoint records, and gather governing contract terms, approvals, policy, and active quality-hold information before a decision is made.
    ```

    ![Enter the skill description](./assets/04.4-skill-description.png)

1. Copy and paste the following in the **Instructions** input then select **Create**:

    ```text
    1. Read the attached invoice and capture its supplier, invoice ID, PO, contract, batch or lot, total, and every line.
    2. Use the configured SharePoint tools (connector actions or MCP) to retrieve the matching invoice, lines, supplier, and quality-event records.
    3. Retrieve governing contract, policy, and written approval content from SharePoint knowledge before making claims about permitted charges or approval requirements. A matching filename, an invoice claim, or correct expected numbers alone do not establish grounding.
    4. Compare the submitted file with current records and retrieved governing evidence. Never resolve missing or conflicting evidence by guessing. If retrieval fails or a source cannot be verified, explicitly record the limitation in missingEvidence or conflictingEvidence and evidenceSummary; set policyUnclear when the governing policy is unavailable or ambiguous. Do not present an unsupported contract-permitted amount as verified.
    5. For each line, identify the invoiced amount and, only when supported by retrieved content, the contract-permitted amount and supporting source. Preserve available document identities, locations, and citation references in evidenceCitations. If standard citations are unavailable, state that limitation and retain whatever source identity and location were actually returned. Never invent facts, source locations, or citations.
    6. Return valid JSON with supplierName, supplierId, invoiceId, purchaseOrder, contractId, invoiceTotal, lineItems, missingEvidence, conflictingEvidence, activeQualityHold, policyUnclear, evidenceSummary, and evidenceCitations. Keep missing or conflicting evidence visible for the decision skill and review brief.
    7. Do not calculate totals, recommend an outcome, or write to SharePoint.
    ```

    > **Screenshot needed:** Capture the Invoice Fact Check Instructions with the updated retrieval, missing/conflicting evidence, and evidenceCitations guidance before selecting Create. Suggested asset: `instructions/assets/04.5-create-skill.png`.

## Upload Invoice Review Decision

1. Select the **Add** icon in the **Skills** section.

    ![Select the add button](./assets/04.1-add-skill-button.png)

1. Leave it on the **Upload a skill** tab and select the **Drag and drop or click to upload** text.

    ![Select the upload button](./assets/04.6-upload-skill.png)

1. Browse to:

    ```text
    D:\LabFiles\skills\invoice-review-decision.zip
    ```

1. Confirm that the skill shows up in the **Skills** section.

    ![Select the skill](./assets/04.7-review-skills.png)

1. Select the **supplier-policy-triage** skill.

    ![Select the skill](./assets/04.8-select-supplier-skill.png)

1. Review the skill and make sure that it has 2 files, a SKILL,md and a calculate_supplier_review.py file. Select the **X** to close out of the skill.

    ![Review the skill](./assets/04.9-skill-review.png)

> [!NOTE]
> **Why:** The uploaded skill demonstrates that a skill can carry executable resources. Python uses decimal-safe arithmetic and creates a PDF in the sandbox.

## Review the submitted invoice

1. Select the **Preview** tab to go back to the testing screen.

    ![Test the changes](./assets/04.10-preview-tab.png)

1. Select the **New chat** button. Select the **Plus Button** and attach:

    ```text
    D:\LabFiles\case-inputs\Caldova_Astor_Ridge_Invoice.xlsx
    ```

    ![Attach the file](./assets/04.11-attach-button.png)

1. Copy and paste the following into the text box and press **Enter**.

    ```text
    Review this Astor Ridge invoice for Finance. Check the submitted charges against current SharePoint records, the governing contract, written approvals, policy, and any active quality hold. Tell me what is supported, what should be challenged, and whether human review is required. Cite the sources and create a review brief. Do not take financial action.
    ```

    ![Send in the prompt](./assets/04.12-send-prompt.png)

1. Inspect the activity and review the action it takes. Select **Approve** for any permissions screens that pop up:
   - attached Excel file read
   - **invoice-fact-check** skill called
   - SharePoint list reads through your configured connector actions or MCP
   - SharePoint knowledge citations
   - **invoice-review-decision** skill called
   - Python execution

    ![Inspect the activity](./assets/04.13-skill-called.png)

1. Check for **$204,600** supported, **$13,100** disputed, **$0** reconciliation difference, no active quality hold, and human review required. Verify that contract and policy claims are backed by retrieved governing content and that the response and brief preserve available source identities, locations, and citations. If retrieval or citations are unavailable, the response must say so and keep missing or conflicting evidence visible; matching the expected amounts alone is not a successful grounding check.

    ![Review the response](./assets/04.14-review-response.png)

1. At the bottom of the response, select the **Caldova_Supplier_Review_ARB-260814.pdf** and open it.

    ![Open the PDF](./assets/04.15-select-pdf.png)

1. Review the PDF and make sure all the data is carried over.

    ![Review the PDF](./assets/04.16-review-pdf.png)

## Record the recommendation

1. In the text input window, copy and paste this follow up message then press **Enter**:

    ```text
    Record this recommendation in the Invoice Review Log with Review Source set to Interactive Agent. Verify that this is a supported choice in the actual list schema and use the configured tool's declared input shape. Ask for my confirmation before creating the item.

    After writing, read the saved item back and report its item ID, Invoice ID, Review Source, Supported Amount, Disputed Amount, and Human Review Required. If the schema or choice value is unavailable, or any required value reads back blank or mismatched, report an incomplete write, not success. Do not take financial action or claim that a person approved the recommendation.
    ```

    > **Screenshot needed:** Capture the updated recording prompt with Review Source = Interactive Agent, confirmation, and read-back requirements visible. Suggested asset: `instructions/assets/04.17-follow-up-prompt.png`.

1. If it struggles to find the Invoice Review Log list, it might ask you for the URL. If it does, provide it with the URL.
1. Review the proposed entry and confirm creation only when the agent has verified the required schema and supported source value. Do not guess internal field names or value shapes to work around missing metadata; report the missing information if the configured tools cannot expose it.
1. Review the response. Open the SharePoint **Invoice Review Log**:

    +++https://@lab.CloudCredential(AITour27M365E7).TenantPrefix.sharepoint.com/sites/CaldovaSupplierOps/Lists/Invoice%20Review%20Log/AllItems.aspx+++

    Verify one ARB-260814 item with Supported Amount **204600**, Disputed Amount **13100**, Human Review Required **Yes**, and Review Source **Interactive Agent**. Compare these with the saved-item read-back, not just the agent's creation message. A blank, missing, mismatched, or unreadable source or amount is an incomplete write, even if the create call returned success. The entry records a recommendation, not payment or human approval; a recorded PDF filename is not an attachment.

    ![Review the log](./assets/04.18-review-log.png)

1. Select **Build** to go back to the configuration screen.

    ![Select the build tab](./assets/04.19-build-tab.png)

Select **Next** to personalize, evaluate and publish the agent.
