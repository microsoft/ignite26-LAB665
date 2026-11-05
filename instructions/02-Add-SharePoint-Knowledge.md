<!-- markdownlint-disable MD034 -->

# 2 - Add SharePoint Knowledge

Contracts, policy, approvals, and quality documents are are the sources that will govern the supplier reviews. You will connect the prepared SharePoint library as agent knowledge.

1. On the agent overview, find **Knowledge** and select **Add knowledge**.

    ![Select the add knowledge button](./assets/02.1-add-knowledge.png)

1. Select **SharePoint**.

    ![Select the SharePoint option](./assets/02.2-select-sharepoint.png)

1. Enter the assigned tenant root site URL then select **Add**:

    +++https://@lab.CloudCredential(AITour27M365E7).TenantPrefix.sharepoint.com/sites/CaldovaSupplierOps+++

    ![Select the add button](./assets/02.3-add-button.png)

1. Review the knowledge details and select **Add to agent**.

    ![Select add to agent button](./assets/02.4-add-to-agent.png)

1. Confirm the knowledge source is now showing in the knowledge section. Select the **Save** icon in the upper right hand corner.

    ![Confirm knowledge](./assets/02.5-confirm-knowledge.png)

> [!NOTE]
> **Why:** Knowledge retrieves relevant information from governed documents. It's different from a connector or MCP tool, which performs live operations against data.

## Test document knowledge grounding

1. Select the **Preview** tab at the top or your agent to open up the testing screen.

    ![Select the preview tab](./assets/02.6-preview-tab.png)

1. Paste the following in the **ask a question or describe what you need** box then press **Enter**:

    ```text
    Under contract CMO-2026-041, what is the maximum expedited-production premium for a $185,000 batch, and what approval is required above that amount?
    ```

    ![Test prompt](./assets/02.7-test-prompt.png)

1. Check that the answer identifies **4%**, **$7,400**, and the need for a **revised purchase order** and written **VP approval**, supported by retrieved governing contract content. These expected numbers alone do not prove the answer is grounded.

    ![Review the response](./assets/02.8-prompt-response.png)

    > [!TIP]
    > Wording can vary. Validate the facts and retrieved source rather than expecting an exact sentence. The screenshots illustrate a grounded answer; they do not prove retrieval succeeded in your session.

1. Open each available **Citation** below the response. Verify that the retrieved contract content supports the premium cap and approval requirement, and check its document identity and location.

    ![Review citations](./assets/02.9-citations.png)

    > [!IMPORTANT]
    > If knowledge retrieval fails, the answer must explicitly report the failure rather than guess the contract terms. If document content was retrieved but standard citations are unavailable, check any available document identity and location and have the agent state the citation limitation. Missing or conflicting governing evidence must remain visible; do not mark this grounding check as passed based on the expected numbers alone. The reported `SubstrateSearch(GetNumActiveUsers)` backend failure is not fixed by these instructions.

1. Select the **Build** tab to go back to the configuration screen.

    ![Select the build tab](./assets/02.10-build-tab.png)

Use the lab navigation to choose one section 3 path: **3 - Add the SharePoint connector**, or **3 - Connect the SharePoint MCP**. Complete only one path, then use the lab navigation to continue to **4 - Add Skills and Review an Invoice**.
