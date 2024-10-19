# Deploying IdentityIQ Using the Services Standard Build (SSB)

The sources provide extensive information on the Services Standard Build (SSB), a toolset designed to streamline the process of building and deploying SailPoint IdentityIQ customizations. While the sources don't explicitly detail a step-by-step deployment guide, they offer valuable insights into the components and procedures involved.

### Core Components and Concepts

*   **Apache Ant:** The SSB utilizes Apache Ant as its primary build tool, relying on XML-based build files to orchestrate tasks. You will need to download and install Ant separately.
*   **Folder Structure:** The SSB enforces a structured directory organization to manage different aspects of the build process. Key folders include:
    *   **`base`:** Contains IdentityIQ product files, patches, and potentially the Accelerator Pack.
    *   **`config`:** Stores configuration objects, organized by type, which represent customizations to be deployed.
    *   **`db`:** Houses customized database scripts used during the build.
    *   **`lib`:** Contains libraries used by the build process but not added to the IdentityIQ installation.
    *   **`scripts`:** Holds all build files, including the master `build.xml` and custom scripts.
    *   **`src`:** Contains custom Java source code to be compiled and included in the build.
    *   **`web`:** Contains content to be directly overlaid onto the IdentityIQ folder structure, such as branding elements, custom web pages, message catalogs, and additional JAR libraries.
*   **Build Configuration:**  The `build.properties` file serves as the central configuration point for the build, defining parameters like IdentityIQ version, database connection details, and application server settings.

### Build Process Overview

1.  **Environment Setup:**
    *   **Download SSB:** Obtain the SSB from Compass.
    *   **Prepare IdentityIQ:** Install IdentityIQ on the development server and ensure prerequisites are met, including necessary permissions and access.
    *   **Export Custom Objects:**  If this is an existing IdentityIQ installation, export custom objects from the development environment. The sources recommend using tools like the Object Exporter task or the IdentityIQ Deployment Accelerator for this purpose.
2.  **Build Directory Population:**
    *   **Place Custom Objects:** Organize exported custom objects in the `config` directory, adhering to the SSB's folder structure.
    *   **Add IdentityIQ Files:** Copy the IdentityIQ product ZIP file and any patch JAR files to the `base` directory.
    *   **Include Plugins:** If using plugins, place their source code in the `pluginsrc` directory.
    *   **Add Custom Java Code:** Put any custom Java code in the `src` directory.
    *   **Include Web Content:** Add any custom web content, branding elements, or additional JAR libraries to the `web` directory.
3.  **Build Configuration:**
    *   **Configure `build.properties`:**  Edit the `build.properties` file to specify build parameters, including the IdentityIQ version, patch level, customer name, JDK path, application server details, and database connection information.
    *   **Create Environment-Specific Properties:** For each target environment (development, test, production), create environment-specific properties files to override default settings and manage environment-specific configurations.
    *   **Handle Sensitive Information:** Utilize `<environment>.target.secret.properties` files to store sensitive data like passwords.
    *   **Define Subset Builds:** If needed, use `<environment>.includefiles.properties` files to specify XML files for subset builds.
    *   **Configure Exclusions:** Employ `<environment>.ignorefiles.properties` files to exclude specific files from the build.
    *   **Manage Keystore Files:**  If using the SSB to deploy keystore files, place environment-specific keystore files (`<environment>.iiq.cfg`, `<environment>.iiq.dat`) at the root of the build directory.
4.  **Build Execution:**
    *   **Set Build Environment:** Set the `SPTARGET` environment variable or use the `servers.properties` file to designate the target environment.
    *   **Run Build Command:** Execute the appropriate Ant target from the command line, such as `build war` to create a deployable WAR file.

### Deployment

After generating the WAR file, deploy it to the target web application server following the server's deployment procedures. The sources provide a brief example for deploying to Tomcat.

### Additional Considerations

*   **Database Setup and Upgrades:** If this is a new IdentityIQ deployment or involves an upgrade, follow the instructions in the IdentityIQ Installation Guide for creating or upgrading the database.
*   **Updating Custom Objects:** To update existing custom objects, use the `build importdynamic` target or manually import the generated `sp.init-custom.xml` file.
*   **Repeatable Initial Builds:** For non-production environments, the SSB supports repeatable initial builds, which involve dropping and recreating the database for clean development iterations.
*   **OWASP Dependency Check:**  The SSB includes the OWASP Dependency Check utility to identify vulnerabilities in third-party libraries used in the build.

By adhering to these steps and leveraging the capabilities of the SSB, organizations can establish a well-defined, automated, and repeatable process for deploying IdentityIQ customizations, leading to greater efficiency, reduced errors, and a more streamlined Identity and Access Management implementation.
