# Resolving Connector Deployment Issues in IdentityIQ

## Resolving Connector Deployment Issues in IdentityIQ

The "Connector-Build-addition-to-SSB.pdf" document outlines a solution to a specific problem encountered when deploying custom connectors in later versions of SailPoint IdentityIQ. The problem stems from the introduction of the `lib-connectors` folder, intended to separate connector code from the main application code. This change, while promoting better organization, **created compatibility issues with existing connectors built using the older `openconnectors` framework.**

### The Problem

Prior to the introduction of the `lib-connectors` folder, custom connectors were typically built as single Plain Old Java Objects (POJOs) and deployed within the `WEB-INF/classes` folder. This approach worked seamlessly in earlier IdentityIQ versions. However, with the introduction of the `lib-connectors` folder, these connectors **no longer function correctly when deployed in the traditional location.**

Attempting to use the older deployment method results in connector failures. This is because IdentityIQ now expects connector code to reside within the `lib-connectors` directory, packaged as JAR files. The shift in directory structure and packaging requirements renders the older connectors incompatible.

### The Proposed Solution

To address this compatibility issue, the "Connector-Build-addition-to-SSB.pdf" document proposes a solution that integrates into the Services Standard Build (SSB) process. The proposed solution involves:

*   **Establishing a Standardized Structure:**
    *   A dedicated folder named `connectorsrc` is created within the SSB base folder to house connector source code.
    *   Each connector is placed within a subfolder named after the connector, mirroring the name of the JAR file to be generated.
    *   Subfolders for `define/applications`, `install/Configuration`, and `src` are created within each connector folder to store XHTML files, registry merge files, and source code, respectively.
*   **Utilizing a Manifest File:**
    *   A `manifest.xml` file is required within each connector's home folder. This manifest file defines key attributes like the connector name, display name, minimum system version, and JAR file dependencies.
    *   The manifest file differs from plugin manifest files by omitting the DTD line and including a specific structure for defining the connector name and JAR file references.
*   **Modifying Build Files:**
    *   Changes are made to the `build.xml` file to incorporate connector build processes. Imports are added to reference the connector build script (`build.connectors.xml`), and properties are defined to locate the `connectorSrc` folder.
    *   Conditional logic is added to the `build.xml` file to execute the connector build process only in IdentityIQ versions where the `lib-connectors` folder exists.
    *   The `build.connectors.xml` file is added to the SSB to manage the connector build process.
    *   Necessary JAR files (`bsf.jar` and `json-simple-1.1.1.jar`) are added to the `lib` folder to support JSON file manipulation during the build.

### The Build Process

The enhanced SSB build process, incorporating the proposed solution, handles connector deployment as follows:

1.  **Verification and Preparation:**
    *   The build process checks for the presence of the `manifest.xml` file in each connector folder.
    *   ConnectorRegistry merge files are copied to the appropriate location within the build's extract folder.
    *   XHTML files for the connectors are copied to their designated location in the build's extract folder.

2.  **Compilation and Deployment:**
    *   The source code within each connector's `src` folder is compiled into a JAR file named after the connector.
    *   The compiled JAR file is copied to the `extract/WEB-INF/lib-connectors` folder within the build.

3.  **JSON File Update:**
    *   An entry is added to the `connectorVsConnectorBundleMapping.json` file, located in the `WEB-INF/lib-connectors` folder.
    *   This entry maps the connector's fully qualified class name to the list of JAR files it depends on, as defined in the `manifest.xml` file.

4.  **Initialization and Finalization:**
    *   After connector deployment, the `build-init` method is re-executed to integrate the added XML files into the `sp.init-custom.xml` file.
    *   The final connector artifacts are placed in the `build/extract/WEB-INF/lib-connector` folder, with additional artifacts generated in the `build/connectors` folder.

### The Solution's Impact

This comprehensive approach ensures that custom connectors built using the `openconnectors` framework can be seamlessly deployed in later IdentityIQ versions. The standardized folder structure, the use of a manifest file, and the modifications to the SSB build process collectively streamline connector deployment and maintain compatibility with the `lib-connectors` structure. By following this process, developers can avoid connector deployment issues and leverage the organizational benefits of separating connector code from the core application code.

