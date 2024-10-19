# Services Standard Deployment

### What are the four build configuration properties that can be specified for different build environments?

The sources provide information about the **build process** for configuring IdentityIQ environments, but they do not explicitly define **four build configuration properties that can be specified for different build environments**.

However, the sources do describe several configuration files and properties that can be customized for different environments, including:

*   **iiq.properties files**: contain properties used by IdentityIQ for connecting to and interacting with its own database. Create separate `<environment>.iiq.properties` files for each environment by copying and editing the product iiq.properties, and place them in the build directory. Examples include `sandbox.iiq.properties`, `test.iiq.properties`, `UAT.iiq.properties`, and `prod.iiq.properties`.
*   **target.properties files**: contain key/value pairs for token substitution during build time. Create a `target.properties` file for each environment. The name of each target.properties file should be in the format `<environment>.target.properties`.  Examples: `sandbox.target.properties`, `test.target.properties`, `UAT.target.properties`, and `prod.target.properties`.
*   **"secret" target.properties files:** can be used to store sensitive token values, like usernames and encrypted passwords, in a separate file that can be excluded from version control systems. The name of the file used for the "secret" target.properties file should be in the format `<environment>.target.secret.properties`.
*   **includefiles.properties files**: can be used to define a 'subset' build, which only includes a specific set of XML files to import into an existing IdentityIQ environment, without deploying an entire build. Create an `includefiles.properties` file for each environment where you want to create a subset build. The file naming pattern is `<environment>.includefiles.properties`.  For instance: `prod.includefiles.properties` or `test.includefiles.properties`.
*   **ignorefiles.properties files:** can be used to define certain XML files that should be skipped during the import for a specific environment.  The file naming pattern is `<environment>.ignorefiles.properties`.  Examples: `prod.ignorefiles.properties` or `test.ignorefiles.properties`.
*   **Log4j properties files:** used to define custom loggers and log levels for each environment. Name them in the format `<environment>.log4j2.properties` or `<environment>.log4j.properties`.
*   **Keystore files:** manage the deployment of encryption keys for each environment. Prefix the names of the keystore files with ‘`<environment>.`’ and place them at the root of the build. For example: `prod.iiq.cfg` and `prod.iiq.dat`.

The sources also mention the `build.properties` file, which specifies important configuration arguments like the IdentityIQ version, customer name, and paths.  This file can be overridden on a per-server or per-environment basis using a separate `<hostname>.build.properties` or `<environment>.build.properties` file.

These various configuration options allow for customization and control over the IdentityIQ build process for different environments, but they do not specifically identify **four build configuration properties** as requested.


### What are the different types of builds that can be performed using the SSB?

Here are the types of builds that can be performed using the SSB, based on the sources you provided:

*   **Full Build:** This type of build generates a complete, deployable WAR file that includes all custom configurations, Java code, and other artifacts. This is the most common type of build and is suitable for deploying IdentityIQ to a new environment or updating an existing one. You can create a WAR file using the `build war` command, which places the WAR file in the `deploy` folder.
*   **Subset Build:** This type of build is used to deploy only a specific set of XML files to an existing IdentityIQ environment without deploying the entire build. To use a subset build, set the `buildSubset` property to `true` in the `build.properties` file and create an `<environment>.includefiles.properties` file listing the XML files you want to include.
*   **Initial Build:** This is a specialized type of build designed for rapidly rebuilding IdentityIQ in a non-production environment. It combines several targets to create an empty database, apply patches, import default and custom artifacts, and deploy the web content. The `initial-build` target encapsulates the necessary steps, and you can chain this target with others as needed. The sources emphasize that this approach is **not recommended for production environments**.

The SSB provides a variety of build targets to support these build types, allowing for flexibility and customization in the deployment process. You can chain these targets together to create a specific build workflow. Some of the commonly used targets include:

*   **clean**: Clears the `build` directory, ensuring a fresh starting point for the build.
*   **createdb**: Creates an empty IdentityIQ database using the credentials in the `<environment>.iiq.properties` file.
*   **extenddb**: Applies named, extended attributes to the database schema.
*   **import-stock**: Imports default IdentityIQ artifacts.
*   **import-lcm**: Imports default IdentityIQ Lifecycle Management artifacts.
*   **import-ap**: Imports artifacts from the Accelerator Pack.
*   **import-custom**: Imports custom XML configuration files from the `config` directory.
*   **patchdb**: Applies database patches if specified in the `build.properties` file.
*   **runUpgrade**: Executes the patch command to update the IdentityIQ database.
*   **dist**: Copies web content, custom Java classes, JDBC drivers, and other files to the appropriate directories in the `build` folder.
*   **cycle**: Restarts the application server.

These build targets and configuration options allow you to create a repeatable and manageable build process for deploying and maintaining your IdentityIQ environment across different stages of development and deployment.



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
