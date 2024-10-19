# Purpose of the IdentityIQ Provisioning Broker

## Purpose of the IdentityIQ Provisioning Broker

The IdentityIQ Provisioning Broker is a crucial element in the IdentityIQ architecture that manages and coordinates changes to user access across different provisioning processes. When a provisioning change is requested, the broker analyzes the request and determines the appropriate provisioning implementation process. It plays a key role in automating and streamlining the provisioning process by intelligently handling various provisioning scenarios.

Here's how the Provisioning Broker works:

*   **Receives Provisioning Requests:** The broker receives provisioning requests from various sources within IdentityIQ, including:
    *   Certifications
    *   Policy violations
    *   Identity Refresh tasks
    *   Lifecycle Manager requests
    *   Lifecycle events

*   **Creates a Provisioning Plan:** Upon receiving a request, the broker creates a comprehensive provisioning plan outlining the necessary actions. This plan details the specific changes needed, such as adding, modifying, or deleting user accounts or entitlements.

*   **Evaluates and Partitions the Plan:** The broker analyzes the provisioning plan and divides it into smaller, manageable plans, often grouping them by target application. This partitioning allows for efficient processing and ensures that each application receives the appropriate instructions.

*   **Determines the Provisioning Mechanism:**  The broker identifies the appropriate mechanism for implementing each partitioned plan. The sources outline three primary provisioning mechanisms:
    *   **Direct Read-Write Connectors:** IdentityIQ uses these connectors to communicate directly with applications that support real-time provisioning. Changes are implemented immediately, and the broker receives confirmation of the action's success.
    *   **Integration Executors:**  These executors handle provisioning for applications that don't support direct, real-time updates. The broker initiates asynchronous processes that may not complete immediately.
    *   **Work Items:** For applications that require manual intervention, the broker creates work items. These work items are assigned to individuals responsible for implementing the changes manually.

*   **Updates the Identity Cube:**  After provisioning actions are completed, the IdentityIQ Identity Cube is updated to reflect the changes. In cases involving direct read-write connectors, the updates are typically reflected immediately. However, for other provisioning mechanisms, an Identity Refresh task might be required to update the Identity Cube.

**Workflows in Provisioning**

Workflows, also known as business processes, are integral to the provisioning process, governing the flow and execution of provisioning requests. These workflows manage the interactions between the Provisioning Broker and other IdentityIQ components, ensuring that requests are processed according to defined business rules and policies.

**Benefits of the Provisioning Broker**

The Provisioning Broker offers several benefits, including:

*   **Automation and Efficiency:** It automates many aspects of the provisioning process, reducing manual effort and improving efficiency.
*   **Centralized Control:**  It provides a central point for managing and coordinating all provisioning activities, ensuring consistency and reducing errors.
*   **Improved Compliance:** By enforcing defined policies and workflows, the broker helps organizations maintain compliance with regulatory requirements.

**Example of the Provisioning Broker in Action**

Let's consider a scenario where a new employee joins the company. An HR system records the new employee's information and triggers a "Joiner" lifecycle event in IdentityIQ. The Provisioning Broker receives the event and initiates the corresponding workflow. This workflow might include tasks such as:

*   Creating a new identity cube for the employee.
*   Assigning business roles based on the employee's job function.
*   Generating provisioning requests for access to various applications.

The broker then partitions the plan based on target applications and utilizes the appropriate provisioning mechanism for each. For example, if the company uses Active Directory, the broker might use a direct read-write connector to create a new user account. However, for an application that requires manual provisioning, the broker would generate a work item for an administrator.

This example demonstrates how the IdentityIQ Provisioning Broker orchestrates and manages the entire provisioning process, ensuring that new employees receive the necessary access in a timely and compliant manner.

