# Advantages of the Services Standard Framework (SSF)

## Advantages of the Services Standard Framework (SSF)

The Services Standard Framework (SSF) is a set of reusable configurations and code objects designed to streamline and simplify the deployment process for IdentityIQ implementations. Here are the key advantages of using the SSF:

*   **Increased Efficiency and Speed:** The SSF offers pre-built components and best practices that eliminate repetitive, low-level development tasks, enabling faster deployment and allowing implementers to focus on customer-specific requirements.
*   **Simplified Deployment:** Frameworks within the SSF abstract common architectures, reducing the complexity of building and configuring IdentityIQ workflows. This simplification makes it easier to manage and maintain the system.
*   **Code Reusability:** The SSF promotes code reuse through its modular design, allowing developers to leverage existing components and configurations across multiple use cases. This reusability saves time and effort while ensuring consistency across the implementation.
*   **Improved Collaboration:** The SSF's structure facilitates collaboration among developers by separating source code from configurable extensions. This separation allows different team members to work on various aspects of the implementation concurrently.
*   **Reduced Testing Efforts:** The SSF components are pre-tested and proven, reducing the amount of testing required during implementation. This saves time and resources while increasing the reliability of the solution.
*   **Enhanced Flexibility and Customization:** While providing standardized components, the SSF also offers configuration options and "hooks" for customization. This allows implementers to tailor the framework to meet specific business needs without sacrificing the benefits of standardization.

The SSF comprises two main categories:

*   **Frameworks:** Plug-and-play components addressing specific aspects of a use case, designed for reusability across multiple scenarios. Examples include:
    *   Field Value Framework: Simplifies provisioning policies by decoupling the logic for setting field values.
    *   Role Assignment Framework: Provides methods to dynamically build account requests for role assignment based on business roles.
    *   Dynamic Emails Framework: Streamlines email queuing and sending from workflows.
    *   Approval Framework: Enables flexible configuration and management of complex approval processes.
    *   Provision Processor Framework: Offers a standardized workflow structure for provisioning processes, handling common tasks like building plans, initializing requests, and managing approvals.

*   **Features:** Complete, configurable, end-to-end use cases, often representing common IdentityIQ functionalities. Features utilize the underlying frameworks to implement their logic. Some features include:
    *   Lifecycle Event (LCE) Features: Address typical identity lifecycle events like Joiners, Movers, Leavers, Rehires, and Attribute Synchronization.
    *   UI Features: Provide workflows accessible through the IdentityIQ user interface, like Terminate Identity.

In addition to the frameworks and features, the SSF includes several tools to further enhance the development and testing process:

*   **Email Template Editor:** Simplifies the creation and management of email templates.
*   **Generic Importer:** Provides a framework for importing various data sources into IdentityIQ.
*   **Mock Integration Executor:** Simulates ticket systems and integration latencies for testing purposes.
*   **Unit Tester:** Facilitates unit testing of IdentityIQ code, such as rules and rule library methods.

The sources highlight the importance of using the SSF within the context of the Services Standard Build (SSB), a set of tools that support the build process for IdentityIQ deployments. The SSB is designed to automate deployment generation, reduce errors, accelerate development, and provide a familiar build structure for developers. The SSF integrates seamlessly with the SSB, leveraging its capabilities for efficient and standardized deployments.

Overall, the SSF provides a comprehensive and robust framework for simplifying, accelerating, and standardizing IdentityIQ implementations. Its modular design, code reusability, and customization options enable developers to build and deploy solutions efficiently while meeting specific business requirements.
