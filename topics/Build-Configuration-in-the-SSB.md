# Build Configuration in the SSB

## Build Configuration in the SSB

The Services Standard Build (SSB) provides a structured and automated approach to building and deploying SailPoint IdentityIQ customizations.  A key aspect of this process is **Build Configuration**, which involves setting up various properties files to tailor the build for different environments and requirements.

### Understanding the build.properties File

The **build.properties** file acts as the central configuration file for the SSB. It contains essential parameters that govern the build process, such as:

*   **IdentityIQ Version and Patch Level:** The `IIQVersion` and `IIQPatchLevel` variables define the specific version and patch level of IdentityIQ used in the build.
*   **Customer or Project Identification:** The `customer` variable helps identify the client or project, especially when generating custom JAR files using the `includeCustomJar` property.
*   **Java Development Kit Path:** The `jdk.home` variable specifies the path to the Java Development Kit (JDK) used for compiling custom Java code. Alternatively, the `JAVA_HOME` environment variable can be used.
*   **Custom Script Execution:** The `runCustomScripts` flag controls the execution of custom build scripts integrated through hook points in the main build process.
*   **Custom JAR Inclusion:** The `includeCustomJar` property determines whether a JAR file containing compiled custom Java classes is created and included in the build.
*   **Application Server Details:** For targets involving application server interaction, variables like `application.server.host`, `application.server.port`, `application.server.start`, and `application.server.stop` define connection details and scripts for starting and stopping the server.
*   **Database Connection Parameters:** To interact with the IdentityIQ database, variables like `db.url`, `db.userid`, `db.password`, `db.driver`, `db.type`, and `db.name` are used, with specific settings for different database types (e.g., `db.db2.*` for DB2, `db.oracle.*` for Oracle).
*   **Safety Prompt Override:** The `override.safety.prompts` flag can be used to disable safety prompts for potentially destructive build targets, particularly useful in automated testing scenarios.

### Supporting Multiple Environments and Platforms

Recognizing that different environments (development, test, production) and platforms (Windows, Linux, Unix) might have distinct requirements, the SSB allows for environment-specific and server-specific properties files.

*   **Environment-Specific Properties:**  Files named `<environment>.build.properties` (e.g., `sandbox.build.properties`) override default settings in the `build.properties` file for a specific environment.
*   **Server-Specific Properties:** Files named `<hostname>.build.properties` (e.g., `sailsandbox.build.properties`) further specialize settings for a particular server within an environment.

This hierarchical approach allows for fine-grained control over build parameters, ensuring consistency and addressing environment-specific needs.

### Environment-Specific Configurations

Beyond the core `build.properties` file, environment-specific settings are managed through:

*   **iiq.properties Files:** These files hold properties used by IdentityIQ for database interactions. Each environment has its own `<environment>.iiq.properties` file, ensuring proper database connections.
*   **target.properties Files:** These files facilitate token replacement during the build process. Environment-specific `<environment>.target.properties` files contain key-value pairs for tokens, allowing for consistent customization across environments.
*   **"Secret" target.properties Files:** For highly sensitive values, such as passwords, environment-specific `<environment>.target.secret.properties` files can be used. These files are typically excluded from version control systems, enhancing security.
*   **includefiles.properties Files:** These files define subset builds, specifying a limited set of XML files to be included in the build. This is particularly useful for deploying incremental changes to an existing IdentityIQ environment.
*   **ignorefiles.properties Files:**  These files define files to be excluded from the build, allowing for environment-specific customization and control over configuration drift.

### Keystore File Deployment

The SSB can manage the deployment of keystore files, which are crucial for encryption and security within IdentityIQ. However, this feature only works if the keystore files are stored in the default location (`WEB-INF/classes/`).

### Setting the Build Environment

The build process needs to know which environment it is targeting. This can be achieved through:

*   **SPTARGET Environment Variable:** Setting the `SPTARGET` environment variable to the desired environment name (e.g., `dev`, `test`, `prod`) directs the build process to use the corresponding environment-specific properties files.
*   **servers.properties File:** If the `SPTARGET` environment variable is not set, the build uses the `servers.properties` file, which maps hostnames to environment names. This approach automatically selects the environment based on the hostname of the machine running the build.

### Considerations and Best Practices

When configuring builds, keep in mind:

*   **Environment Separation:** Properly separate configurations for different environments to avoid conflicts and ensure consistency.
*   **Security:** Encrypt sensitive information and use "secret" target.properties files to protect confidential data.
*   **Version Control:** Utilize a version control system to track changes and facilitate collaboration.
*   **Documentation:** Thoroughly document build configurations to aid understanding and maintainability.

By adhering to these principles and leveraging the features of the SSB, organizations can establish a robust and repeatable build process, streamlining IdentityIQ deployments and enhancing the overall efficiency of their Identity and Access Management operations.
