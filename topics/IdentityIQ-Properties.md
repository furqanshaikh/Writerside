# IdentityIQ Properties

Let's explore the contents of the file *iiq.properties* based on the provided sources.

### Understanding *iiq.properties*

The *iiq.properties* file plays a critical role in the configuration of IdentityIQ. It houses various settings that control the application's behavior and interaction with databases and other components.

*   **Location:** You can find this file in the *identityiq\_home\WEB-INF\classes* directory, where *identityiq\_home* represents the location where the *identityiq.war* file was expanded.
*   **Database Configuration:** One of the crucial aspects managed within *iiq.properties* is database connectivity. It holds parameters such as Host Name, Database Type, Database Name, User ID, and Password, which are essential for IdentityIQ to communicate with its databases.
*   **Plugin Management:** Parameters related to plugins are also present in *iiq.properties*. The settings *plugins.runSqlScripts*, *plugins.importObjects*, and *plugins.enabled* govern plugin behavior. For instance, setting these values to *false* would entirely disable plugins within IdentityIQ.
*   **JNDI Configuration:** The file can also contain JNDI settings for defining and managing data sources used by IdentityIQ.
*   **Keystore Configuration:** The location of the keystore file (*iiq.dat*) and password file (*iiq.cfg*) can be specified in *iiq.properties* using *keyStore.file* and *keyStore.passwordFile* respectively. However, these options are commented out by default. The keystore is crucial for encryption and security within IdentityIQ.
*   **Embedded Broker Configuration:** If using the embedded broker, *iiq.properties* allows you to customize its memory and disk usage.

### Important Considerations

*   **Upgrading:** When upgrading IdentityIQ, it's strongly advised to use the *iiq.properties* file provided with the new version. This helps prevent complications arising from changes in variables between versions.
*   **Backup:** Creating backups of *iiq.dat* and *iiq.cfg* is essential. This ensures you can easily restore them in case of upgrades or reinstallation of IdentityIQ.

The sources also mention additional files and commands that interact with *iiq.properties*:

*   **Extended Attribute Configuration:** To customize extended attributes, you need to edit XML files such as *IdentityExtended.hbm.xml*, *LinkExtended.hbm.xml*, and *CertificationItemExtended.hbm.xml*. These modifications need to be reflected in the database by using the *iiq script* to run the *schema* command.
*   **IdentityIQ Console:** This command-line tool, launched using *iiq.bat*, interacts with IdentityIQ's configuration. Commands such as *properties* can display the content of *iiq.properties*.

By understanding these points, you can effectively configure IdentityIQ using the *iiq.properties* file and associated tools.

