<!-- markdownlint-disable MD034 -->

# 3 - Add the SharePoint connector

Now you'll enable your agent to perform actions by adding SharePoint connector tools. Use this path as an alternative when the SharePoint MCP is unavailable or unreliable.

Use the lab navigation to choose either this section or **3 - Connect the SharePoint MCP**, not both. After completing your chosen path, use the lab navigation to continue to **4 - Add Skills and Review an Invoice**.

## Add the SharePoint actions

1. Select the **Plus button** in the **Tools** section.

    ![Select the add button](./assets/03.1-add-tool.png)

1. Select the **Connectors** tab.

    ![Select the Connectors tab](./assets/03.2-connector-tab.png)

1. Type `SharePoint Get` in the text box. The **SharePoint** group may show only a partial list of actions. If **Get item** is not visible, select **See N more** next to **SharePoint** to expand the group, then select **Get item**. The number in **See N more** varies.

    > **Screenshot needed:** Capture the Connectors search for `SharePoint Get` with the collapsed SharePoint group and its **See N more** expansion link visible. Suggested asset: `instructions/assets/03.3-expand-sharepoint-actions.png`.

    ![Select SharePoint Get item](./assets/03.3-select-get-item.png)

1. Select the **Add** button.

    ![Add Get item](./assets/03.4-add-get-item.png)

1. Select the **Plus button** in the **Tools** section again.

    ![Select the add button](./assets/03.5-plus-tool.png)

1. Select the **Connectors** tab and search for `SharePoint Get`. If **Get items** is not visible in the partial **SharePoint** group, select **See N more** (the count varies) to expand it, then select **Get items**.

    ![Select SharePoint Get items](./assets/03.3-select-get-items.png)

1. Select the **Add** button.

    ![Add Get items](./assets/03.4-add-get-items.png)

    > [!IMPORTANT]
    > **Get item** reads a single record by its numeric SharePoint item ID. **Get items** lets the agent find matching supplier, invoice, invoice-line, quality-event, and existing request records when that ID is not yet known. Add both so the review can find records before reading or updating them.

1. Select the **Plus button** in the **Tools** section again, then select the **Connectors** tab.

1. Type `SharePoint Create` in the text box. If **Create item** is not visible in the partial **SharePoint** group, select **See N more** (the count varies) to expand it, then select **Create item**.

    ![Select SharePoint Create item](./assets/03.6-select-create-item.png)

1. Select the **Add** button.

    ![Add Create item](./assets/03.7-add-create-item.png)

1. Select the **Plus button** in the **Tools** section again.

    ![Select the add button](./assets/03.8-add-tool.png)

1. Select the **Connectors** tab.

    ![Select the Connectors tab](./assets/03.2-connector-tab.png)

1. Type `SharePoint Update` in the text box. If **Update item** is not visible in the partial **SharePoint** group, select **See N more** (the count varies) to expand it, then select **Update item**.

    ![Select SharePoint Update item](./assets/03.9-select-update-item.png)

1. Select the **Add** button.

    ![Add Update item](./assets/03.10-add-update-item.png)

1. Select the **Save** icon to save your changes.

    ![Save the changes](./assets/03.11-save.png)

1. Select the **Plus button** in the **Tools** section again.

    ![Select the add button](./assets/03.11-plus-button.png)

1. Select the **Connectors** tab.

    ![Select the Connectors tab](./assets/03.2-connector-tab.png)

1. Type `SharePoint Get` in the text box. If **Get lists** is not visible in the partial **SharePoint** group, select **See N more** (the count varies) to expand it, then select **Get lists**.

    ![Select SharePoint Get lists](./assets/03.12-select-get-lists.png)

1. Select the **Add** button.

    ![Add Get lists](./assets/03.13-add-get-lists.png)

1. Select the **Save** icon to save your changes.

    ![Save the changes](./assets/03.14-save.png)

> [!NOTE]
> Use the prepared site for SharePoint actions:
>
> +++https://@lab.CloudCredential(AITour27M365E7).TenantPrefix.sharepoint.com/sites/CaldovaSupplierOps+++
>
> If prompted for a connection, sign in with your assigned Microsoft 365 account. The agent can use **Get lists** to discover the site's lists and **Get items** to locate records. Do not add delete or sharing actions. Keep the agent's confirmation requirement for writing to the Invoice Review Log.

## Start a supplier invoice review

1. Select the **Preview** tab to go back to the testing screen.

    ![Test the changes](./assets/03.9-preview-tab.png)

1. Select the **New chat** button. Copy and paste the following into the text box and press **Enter**.

    ```text
    Astor Ridge Biologics has asked us to review invoice ARB-260814.

    Verify that the supplier is active and whether batch CDV-AX47 has an active quality hold. If the supplier is active and there is no active hold:
    1. Update invoice ARB-260814 from Pending Review to Review Requested.
    2. Look for an Invoice Review Requests item whose Title is Astor Ridge invoice review - ARB-260814. If it does not exist, create it. If it already exists, update it instead so there is only one request.
    3. Set Invoice ID to ARB-260814, Request Notes to Review the expedited production premium, cold-chain freight, and validation documentation charges against the contract, approvals, policy, and quality records, and Status to New.

    Read the invoice and request back. Report the supplier and quality checks, the invoice's new status, the request item ID, and whether you created or updated the request. Do not analyze the contract or decide which charges are supported yet.
    ```

    ![Enter the request](./assets/03.10-test-prompt.png)

1. If prompted, select **Approve** in the **Permission Required** message to call the SharePoint tools.

    ![Approve the tool request](./assets/03.11-approve-mcp.png)

    > [!NOTE]
    > The remaining screenshots show the shared review flow captured with MCP. On this path, the tool names and permission details will instead reflect the SharePoint connector actions.

1. Confirm the response reports an active supplier, no active quality hold, invoice status Review Requested, and the request item ID.

    ![Review the response](./assets/03.12-review-response.png)

1. Open the **Invoice Review Requests** list:

    +++https://@lab.CloudCredential(AITour27M365E7).TenantPrefix.sharepoint.com/sites/CaldovaSupplierOps/Lists/Invoice%20Review%20Requests/AllItems.aspx+++

    Verify one **Astor Ridge invoice review - ARB-260814** item has Status **New** and the specified request notes.

    ![Review the list](./assets/03.13-view-list-item.png)

1. Select the **Build** tab to go back to the configuration screen.

    ![Go back to the build tab](./assets/03.14-build-tab.png)

This completes the connector path for section 3. Use the lab navigation to continue to **4 - Add Skills and Review an Invoice**; skip the alternative **3 - Connect the SharePoint MCP** page.
