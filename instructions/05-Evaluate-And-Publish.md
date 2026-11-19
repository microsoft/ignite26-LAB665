# 5 - Personalize, Evaluate and Publish the Agent

Now we'll see how to add a layer of personalization to the agent with memories. Then we'll do some more thorough testing with evaluations and publish our agent.

## Enable preference-only memory

1. In the **Build** tab of your agent, locate the **Memory** section and toggle the setting to **On**.

    ![Turn memory on](./assets/05.1-memory-on.png)

1. Select the **Save** icon in the upper-right corner.

    ![Save the changes](./assets/05.2-save.png)

1. Select the **Preview** tab.

    ![Select preview](./assets/05.3-preview.png)

1. Select the **New chat** button to start a fresh chat. Copy and paste the following into the input window to have the agent save a memory:

    ```text
    Remember that I am based in London. Use UK date and time conventions, and put anything that needs my attention first under a heading called My actions.
    ```

    ![Save a memory](./assets/05.4-memory-prompt.png)

1. Verify you get a confirmation that the memory was saved. Select the **Manage Memories** button.

    ![Manage memories](./assets/05.5-manage-memories.png)

1. Verify that the memory was saved. Close out of the tab and go back to the tab that your agent is in.

    ![Verify memory](./assets/05.6-review-memory.png)

1. Select the **New chat** button to start a fresh chat. Copy and paste the following into the input window:

    ```text
    Give me the Astor Ridge ARB-260814 review result. Include the invoice date.
    ```

    ![Test memory](./assets/05.7-test-memory.png)

1. Confirm the response puts required attention under **My actions** and shows the invoice date using a UK format such as **14 August 2026**, not **08/14/2026**.

    ![Review the response](./assets/05.8-review-memory-test.png)

    > [!NOTE]
    > Only the communication preferences should come from memory. Confirm that the agent retrieves the review result and invoice date from current SharePoint records rather than remembering case facts from the previous chat.

1. Go back to the tab where you were configuring your agent in Copilot Studio. Select the **Build** tab to go back to the configuration screen.

    ![Go back to the build tab](./assets/05.9-build-tab.png)

> [!IMPORTANT]
> **Why:** Location, date format, and personal working style are durable user preferences. Supplier facts, approval limits, case decisions, and quality status can change and must never come from memory.

## Configure Settings

Now let's take a look at some settings to personalize the agent even further.

1. Select the **three dots (...)** in the upper-right corner, then select **Settings**.

    ![Open settings](./assets/02.1-settings.png)

1. Select the **Greetings & prompts** tab.

    ![Select greetings & prompts](./assets/02.2-greetings.png)

1. Copy and paste the following in the **Greeting message** box:

    ```text
    Hello! I can help review supplier invoices against available contracts, approvals, and quality information, explain supported and disputed charges, and create a review brief. Attach an invoice or provide an invoice ID to begin. Financial decisions remain with an authorized reviewer.
    ```

    ![Greeting message](./assets/02.3-greeting-message.png)

1. Select **Add a suggested prompt**.

    ![Add suggested prompt](./assets/02.4-add-prompt.png)

1. In the **Title** input, paste in `Review invoice`. In the **Message** input, paste in `Review an attached supplier invoice and create a review brief.`

    ![Review invoice prompt](./assets/02.5-invoice-prompt.png)

1. Select **Add a suggested prompt** again.

    ![Add second prompt](./assets/02.6-add-second-prompt.png)

1. In the **Title** input, paste in `Explain a disputed charge`. In the **Message** input, paste in `Explain why a charge on the attached invoice should be challenged. Show the invoiced amount, the amount supported by evidence, and what would resolve the dispute.`

    ![Explain dispute prompt](./assets/02.6-second-prompt.png)

1. Select **Done** to close out of the agent settings.

    ![Select done](./assets/02.7-settings-done.png)

1. Select the **Save icon** to save your agent settings.

    ![Save](./assets/02.7-save.png)

1. Select the **Preview** tab and notice how your custom greeting and starter prompts now show up.

    ![Review](./assets/02.8-preview-greeting.png)

## Evaluate the configured agent

1. Select the **Evaluate** tab.

1. If the evaluation setup is not already open, select **Create your first evaluation**.

    ![Create eval](./assets/05.11-create-eval.png)

1. At the top of the setup page, select **Enter the evaluation name** and name it `Supplier Assurance baseline`.

    ![Set eval name](./assets/05.12-eval-name.png)

1. In **Create or select a data set**, select **Import**. Under **Select data type**, change the default to **Conversations** before uploading the CSV.

    ![Eval configuration](./assets/05.13-eval-config.png)

1. In the upload area, select **browse** and upload:

    ```text
    D:\LabFiles\evaluation\Supplier-Assurance-Baseline.csv
    ```

    > [!IMPORTANT]
    > If you uploaded while **Single responses** was selected, select **Conversations** and upload the CSV again. Changing the data type alone does not reprocess the earlier upload or clear its validation error. Do not continue until the new upload succeeds.

1. In **Review data set**, confirm the successful upload contains exactly two conversations: **Review Astor Ridge invoice ARB-260814** and the question about whether a disputed amount of exactly **$10,000** requires human review based on the amount alone.

    ![Eval data set](./assets/05.14-eval-data-set.png)

1. In **Select test methods**, make sure **General quality** is set.

    ![Eval general quality](./assets/05.15-gen-quality.png)

1. In **Additional configuration**, review **Connections**. Select **Connect Tool** (or **Connect N tools**, depending on the selected path), authenticate the configured SharePoint tools with your assigned account if prompted, then select **Save** in the pop-up. Confirm that all required tools are connected before running the evaluation.

    ![Eval connections](./assets/05.15-conections.png)

1. Select the **Save** icon to save the named evaluation configuration.

    ![Save eval](./assets/05.16-save-eval.png)

1. Select **Run** to start the evaluation.

    ![Run eval](./assets/05.17-run-eval.png)

    > [!NOTE]
    > The evaluation can take 5-10 minutes to run.

1. Wait for the run to complete, then review the results for both conversations. Check for **passed** results; inspect any failures rather than treating an incomplete run or a failed check as success.

    ![Eval results](./assets/05.18-eval-pass.png)

1. Select the **Review Astor Ridge invoice ARB-260814** conversation.

1. Review the conversation flow, paying attention to the knowledge used and tools called. Confirm:
   - Supported amount **$204,600**, disputed amount **$13,100**, and reconciliation difference **$0**.
   - Human review is required because the disputed amount exceeds **$10,000**, with no active quality hold.
   - Contract and policy claims are grounded in retrieved content, and missing evidence or citation limitations remain visible.
   - Both **invoice-fact-check** and **supplier-policy-triage** are used.
   - Any Invoice Review Log creation happens only after explicit confirmation; no financial or supplier action is taken.

    No invoice file is attached in this evaluation. The agent should explicitly state that it used SharePoint invoice records instead of comparing an attachment. Select the **X** to close the conversation.

    ![Review eval](./assets/05.19-review-eval.png)

1. Open the **$10,000** boundary-question conversation. Confirm that the answer says a disputed amount of **exactly $10,000 does not require human review based on the amount alone**. The amount-based rule applies above $10,000; other policy conditions may still require human review. Verify the policy citation, then close the conversation.

> [!NOTE]
> **Why:** A multi-turn conversation tests whether the agent maintains case context while preserving its grounding and action guardrails. General quality evaluates the conversation without requiring identical wording, but a passing score does not replace the amount, evidence, and confirmation checks above. Investigate discrepancies before publishing.

## Publish

1. Select the **Publish** button in the upper-right corner to open the publishing dialog.

    ![Publish the agent](./assets/05.20-publish.png)

1. In the dialog, select the **Publish agent** button. Select the **Done** button after publishing is complete.

    ![Publish the agent](./assets/05.21-publish.png)

Select **Next** to build the workflow.
