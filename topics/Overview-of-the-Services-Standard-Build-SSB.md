# Overview of the Services Standard Build (SSB)

The Services Standard Build (SSB) is a set of tools designed by SailPoint Services to improve the process of building and deploying customized IdentityIQ environments. The SSB is a subset of the Services Standard Deployment (SSD) and is focused on the build process.

### Benefits of the SSB

The SSB aims to achieve the following goals:

*   **Automation:** Automates the creation of deployments for various environments such as development, testing, UAT, and production
*   **Standardization:** Offers a consistent project structure that reduces onboarding time for new team members
*   **Error Reduction:** Reduces the likelihood of deployment errors due to incorrect configurations, patches, or efixes
*   **Faster Development:** Provides useful tools and methods to streamline the IdentityIQ configuration process
*   **Replication:** Enables the SailPoint support team to easily replicate IdentityIQ environments
*   **Familiarity:** Presents a build structure that is familiar to J2EE and servlet application developers

### Components of the SSB

The SSB uses Apache Ant, along with ant-contrib 1.0b3 and catalina-ant, to execute build scripts.

*   **Apache Ant:** The primary build tool that uses XML documents to define build instructions. You will need to download Ant separately as it is no longer included in the SSB.
*   **Ant Contrib:** Provides extensions for Ant, such as custom tasks like `<if><then>` blocks.
*   **Catalina-Ant:** Used for interactions with Tomcat application servers.
*   **Custom Ant Tasks:** The SSB includes custom Ant task extensions developed by SailPoint.

### Process Overview

The process of using the SSB involves several steps:

1.  **Download:** Download the SSB from Compass and extract it into a directory accessible to your development environment.
2.  **Export Custom Objects:** Export the custom objects from your development environment (not applicable for new IdentityIQ installations).
3.  **Setup Directory Structure:** Organize the build directory according to the SSB structure.
4.  **Configure the Build:** Modify the `build.properties` file and other environment-specific properties files to define build parameters.
5.  **Run the Build Command:** Execute the appropriate Ant target to generate the IdentityIQ deployment artifact (WAR file).

### Key Concepts and Features

*   **Folder Structure:** The SSB has a defined folder structure with specific directories for base files, custom code, plugins, configuration objects, and build outputs.
*   **Configuration Objects:**  All environment configurations are placed in the `<SSB install directory>/config` directory, organized by object type.
*   **Plugins:** The SSB supports building and deploying plugins, which are placed in the `pluginsrc` directory.
*   **Build Configuration:** The `build.properties` file holds key build parameters like IdentityIQ version, database settings, and application server details.
*   **Environment-Specific Properties:** Files named `<environment>.build.properties` and `<hostname>.build.properties` allow customizing build settings for different environments and servers.
*   **Environment-Specific Configurations:**  The SSB uses `<environment>.iiq.properties`, `<environment>.target.properties`, `<environment>.target.secret.properties`, `<environment>.includefiles.properties`, and `<environment>.ignorefiles.properties` files to manage environment-specific settings, token replacement, sensitive information, subset builds, and file exclusions.
*   **Keystore File Deployment:**  Keystore files for encryption are typically placed in `WEB-INF/classes/`.
*   **Setting the Build Environment:**  The build environment is determined using either the `SPTARGET` environment variable or the `servers.properties` file.
*   **Build Targets:** The SSB offers various Ant targets to execute different build tasks, such as `clean`, `main`, `dist`, `createdb`, `dropdb`, `extenddb`, `import-stock`, `import-custom`, `cycle`, `initial-build`, and more.

### Services Standard Frameworks (SSF)

The SSB is designed to be used in conjunction with the SSF, which provides a set of reusable IdentityIQ configurations and code objects. The SSF includes:

*   **Frameworks:** Plug-and-play components that address common use cases, such as Field Value, Role Assignment, Email, and Approval.
*   **Features:** End-to-end solutions for specific business requirements, including lifecycle events like Joiner, Leaver, Attribute Synch, Mover, Rehire, and UI features like Terminate Identity.

### Example SSF Tools

The sources you've provided mention several SSF tools:

*   **Certification Closer:** Allows closing certifications and setting their status to complete.
*   **Email Template Editor:** Provides a way to manage and edit email templates.
*   **Enhanced Email Notifier:** Extends email notification capabilities with features like dynamic templates and summary emails.
*   **Generic Importer:** Offers a flexible framework for importing data from various sources.
*   **Mock Integration Executor:** Enables testing integrations using mock data.
*   **Password Expiration Reminder:** Facilitates sending password expiration reminders to users.
*   **Workgroup Migrator:** Allows migrating workgroups between IdentityIQ environments.
*   **SST Unit Tester:** Provides a framework for unit testing IdentityIQ code, such as rules and rule library methods.

### Conclusion

The SSB, along with the SSD and its various components, provides a comprehensive and standardized approach to building, deploying, and testing IdentityIQ customizations. By leveraging these tools and frameworks, organizations can streamline their Identity and Access Management implementations, reduce errors, and accelerate their development cycles.
