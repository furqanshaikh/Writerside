# Overview of the IdentityIQ Accelerator Pack

## Overview of the IdentityIQ Accelerator Pack

The IdentityIQ Accelerator Pack is a set of pre-built configurations and components designed to simplify and expedite IdentityIQ implementations. The sources highlight several key aspects of the Accelerator Pack:

*   **Purpose and Benefits:** The Accelerator Pack aims to reduce deployment time and cost by providing pre-configured solutions for common Identity and Access Management (IAM) requirements. It offers a user-friendly interface that simplifies complex processes, enabling business analysts to configure and manage various aspects of IdentityIQ without extensive technical expertise.

*   **Components:** The Accelerator Pack includes a range of features, categorized as Frameworks and Features, to address different facets of IAM.

    *   **Frameworks:** These are reusable building blocks designed to be integrated into various use cases. Examples mentioned in the sources include:
        *   **Field Value Framework:** Streamlines the process of setting and managing identity attribute values.
        *   **Role Assignment Framework:** Simplifies the assignment of roles and entitlements to identities based on defined rules and criteria.
        *   **Email Framework:** Provides a standardized mechanism for sending email notifications, supporting dynamic content and customization.
        *   **Approval Framework:** Facilitates configuring and managing approval workflows for different types of requests, including access requests and lifecycle events.
    *   **Features:** Features are complete, end-to-end solutions for specific business requirements, often built upon the underlying Frameworks. The sources provide details on:
        *   **Lifecycle Event Features:** These address common lifecycle events like:
            *   **Joiner:** Automates the onboarding process for new employees, including provisioning of initial access.
            *   **Leaver:** Manages the offboarding process for departing employees, ensuring timely revocation of access and account deactivation.
            *   **Attribute Synch:** Enables synchronizing attribute changes between IdentityIQ and target systems, maintaining data consistency.
            *   **Mover:** Handles employee transfers within the organization, automating access adjustments based on the new role or department.
            *   **Rehire:** Facilitates the re-onboarding of previously terminated employees, potentially restoring prior access.
        *   **UI Features:** Examples include:
            *   **Terminate Identity:** Provides a streamlined interface for initiating the termination process for an identity, potentially triggering the Leaver feature.

*   **Configuration and Deployment:** The Accelerator Pack offers a GUI-driven configuration interface, abstracting much of the underlying complexity. However, this abstraction can pose challenges when tracking changes and integrating them into the SSB.

    *   **Deployment with the SSB:** The SSB supports deploying the Accelerator Pack. The process involves placing the Accelerator Pack ZIP file in the `base/ap` directory of the SSB, setting the `deployAcceleratorPack` property in `build.properties` to `true`, and merging the Accelerator Pack's Hibernate files and `iiqCustom.properties` with existing customized versions. This merge process often requires manual intervention.

*   **Updates and Versioning:** When updating the Accelerator Pack configuration, it's crucial to track the modified objects for proper version control and build integration. The sources recommend using the XML Object Exporter or the Export Script to export only the objects that have changed since a specific time, allowing for targeted updates within the build.
*   **Beta Functionality:** The Accelerator Pack includes Beta features that require separate initialization steps. Users need to import specific XML files, often through the IdentityIQ console, to activate and configure these Beta features.
*   **Availability:** The latest version of the Accelerator Pack can be downloaded from the SailPoint Compass community site.

The Accelerator Pack is designed to complement the SSB, providing pre-built solutions that can be readily integrated into the build and deployment process. By leveraging the Accelerator Pack's features, organizations can significantly accelerate their IdentityIQ implementations, focusing more on business requirements and less on technical configuration details.
