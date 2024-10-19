# Mock Integration Executor

## How the Mock Integration Executor Works with IdentityIQ Workflows

The Mock Integration Executor simulates a ticket system within your IdentityIQ development environment, allowing you to test integration-related workflows and features without a real ticketing system. It's also helpful for simulating high-latency provisioning scenarios.

Here's a breakdown of how it works:

*   **Integration with Workflows:** The Mock Integration Executor interacts with IdentityIQ workflows in the same manner as any other integration. For example, during the "Approve and Provision" stage of an access request workflow, the Mock Integration Executor mimics opening a ticket.
*   **Simulating Ticket Creation:**  When an access request is submitted, approved, and reaches the "Approve and Provision" stage:
    *   The Mock Integration Executor adds an entry to the tickets map within the MockIntegration Custom object, simulating the creation of a ticket.
    *   The ticket number corresponds to the access request number, and the initial status is set to "queued."
    *   If the MockIntegration Custom object doesn't exist, the Mock Integration Executor automatically creates it.
*   **Manually Updating Ticket Status:**  To proceed with the simulated provisioning process, you need to manually change the ticket status from "queued" to "committed." This is typically done using the IdentityIQ debug screen.
*   **Provisioning and Status Check:** The "Perform Maintenance" task in IdentityIQ includes a workflow called "Check Status of Queued Items." When this workflow runs, it processes the simulated tickets.
    *   The Access Request UI will display the status as "finished" once the simulated provisioning is complete.
*   **Simulating Latency:** To test how IdentityIQ handles delays in provisioning, the Mock Integration Executor includes a `simulatedLatency` setting. This setting introduces a pause (in milliseconds) at the beginning of any provisioning or status check operation, mimicking the latency of a real ticketing system.

**Default Behavior and Configuration:**

By default, IdentityIQ checks ticket status hourly, even if the "Perform Maintenance" task runs more frequently. You can adjust the `provisioningStatusCheckInterval` variable in the "Check Status of Queued Items" workflow script to increase the frequency of status checks during development.

The Mock Integration Executor offers a configuration option called `assumeSuccessfulTicketOperations`. When enabled, this option automatically sets the ticket status to "queued" upon provisioning and transitions it to "committed" during the first status check. While convenient for bypassing manual status updates, this effectively opens and closes the ticket within the provisioning step, preventing the workflow from reaching the "check status" stage.

**Configuration Options:**

The Mock Integration Executor uses the `IntegrationConfig` object for configuration. Key settings include:

*   `assumeSuccessfulTicketOperations`:  Controls whether ticket status updates are handled automatically (true) or manually (false).
*   `customObjectName`:  Specifies the name of the Custom object used to store the simulated tickets.
*   `simulatedLatency`: Defines the artificial delay (in milliseconds) for simulating provisioning latency.

**Generic Integration Configuration:**

The `IntegrationConfig` object also supports generic settings applicable to all integrations, including the Mock Integration Executor. Two examples of such settings are:

*   `ManagedResources`: Used to specify resources managed by the integration.
*   `StatusMap`: Maps statuses from the external system (in this case, the simulated ticket system) to the internal IdentityIQ statuses.

By leveraging these configuration options, you can tailor the Mock Integration Executor to your specific testing needs, enabling you to effectively validate integration-related workflows and simulate different provisioning scenarios.
