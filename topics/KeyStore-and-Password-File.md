# KeyStore and Password File

Let's discuss the keystore file (*iiq.dat*) and password file (*iiq.cfg*) within the context of IdentityIQ, using the information provided in the sources.

### Keystore and Password Files: Core Security Components

**The keystore file (*iiq.dat*) and password file (*iiq.cfg*) form the foundation of IdentityIQ's data encryption mechanism.** They ensure that sensitive information, such as passwords and application secrets, remains protected.

*   **KeyStore:** The keystore (*iiq.dat*) is a secure repository that stores encryption keys used by IdentityIQ. It acts as a central hub for managing and safeguarding these keys.
*   **Master Password:** A master password protects the entire keystore. It serves as a high-level encryption layer, adding an additional layer of security to the stored encryption keys.

### Default Location and Alternative Paths

**By default, both files reside in the following location:**

```
keystorePassword = WEB-INF/classes/iiq.cfg
keystore = WEB-INF/classes/iiq.dat 
```

**However, IdentityIQ allows for flexibility by offering alternative locations for these files.** You can specify custom paths in the *iiq.properties* file using the following keys:

*   `keyStore.file`: Defines the location of the keystore (*iiq.dat*)
*   `keyStore.passwordFile`: Defines the location of the master password file (*iiq.cfg*)

This flexibility proves beneficial when managing multiple IdentityIQ instances or adhering to specific security policies.

### Keystore Console: Command-Line Interface for Key Management

IdentityIQ provides a command-line tool known as the **Keystore Console**, accessed via the `iiq keystore` command. This console allows administrators to perform various key management operations, including:

*   **Creating a New Key (`addKey`):** Generates a new encryption key, enhancing security by enabling site-specific encryption.
*   **Listing Keystore Contents (`list`):** Displays the contents of the keystore, providing an overview of stored keys and their properties.
*   **Changing the Master Password (`master`):** Updates the master password, ensuring ongoing protection of the keystore. Offers options for manually setting a new password or generating one.

### Encrypted Data Synchronization: Maintaining Data Integrity

When a new encryption key is added to the keystore, existing passwords might still be decryptable using older methods. To address this vulnerability, IdentityIQ provides the **Encrypted Data Synchronization Task**. This task re-encrypts data using the latest key in the keystore, guaranteeing data integrity and protection.

### Best Practices and Considerations

*   **Security Best Practices:** Strict file permissions are crucial for *iiq.dat* and *iiq.cfg*. Access should be limited to the application server running IdentityIQ to prevent unauthorized decryption attempts.
*   **Backup and Restore:** Regular backups of *iiq.dat* and *iiq.cfg* are vital, especially before upgrades or reinstallations. This ensures the availability of encryption keys and prevents data loss in case of system failures or errors.
*   **Site-Specific Encryption:** The keystore feature enables site-specific encryption, preventing passwords from being decrypted on different IdentityIQ installations. This enhances security by isolating encryption keys to specific environments.

By understanding these key concepts and practices, you can effectively manage and maintain the security of sensitive data within your IdentityIQ implementation.
