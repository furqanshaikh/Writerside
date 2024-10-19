# Credential Cycling Configuration Types

### Credential Cycling Configuration Types

The sources mention three types of credential cycling configurations in IdentityIQ:

*   **BeyondTrust Credential Cycling Configuration:**  This configuration allows applications to retrieve credentials from a BeyondTrust PowerBroker Password Safe vault at runtime. You need to define which applications will use credential cycling, specify the PAM solution, and configure how each application contacts the BeyondTrust repository. The sources note that passwords for BeyondTrust PowerBroker Password Safe applications must be in JSON format. For example:

    ```json
    {"bt_user":"MyUserName","bt_password":"MyPasswordValue"}
    ```

*   **CyberArk Credential Cycling Configuration:** Similar to the BeyondTrust configuration, this setup enables applications to fetch credentials from CyberArk Digital Vaults during runtime. This configuration requires installing the CyberArk Credential Provider API on the IdentityIQ server. A configuration template is provided for defining the applications using credential cycling, CyberArk source values, and the mapping between source values and IdentityIQ application fields for authentication.
*   **Direct Mapping Credential Cycling Configuration:**  This option provides a solution-neutral approach for direct attribute mapping when not relying on a third-party PAM source like BeyondTrust or CyberArk. You configure your actual credential values directly within the `Credential Source` section of the template. It's recommended to use encrypted passwords for enhanced security in this scenario.

The sources emphasize that when credential cycling is enabled for an application, the Connection User and Connection Password fields on the Application Definition page can be left blank or populated with dummy values as they will be retrieved during runtime. 
