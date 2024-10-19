# Three Types of IdentityIQ Provisioning Policies

### Three Types of IdentityIQ Provisioning Policies

The sources provide information about **three main types of IdentityIQ provisioning policies**:

*   **Create:** These policies outline the attributes needed to create a new account on a target system. When a user requests access that requires a new account, IdentityIQ pulls the required attributes from the Create provisioning policy and incorporates them into the provisioning plan. For instance, when provisioning a new account on an LDAP application, the Create policy would include mandatory attributes like username and email. Optional attributes can be included to set additional values as per business requirements.
*   **Update:** Update provisioning policies define the attributes that can be modified when updating existing accounts. They specify how the values of these attributes should be provided, whether manually by an IdentityIQ user or automatically through rules or scripts.
*   **Delete:** These policies govern the process of deleting accounts from target systems. They specify any conditions or actions that need to be met or executed before an account is deleted.

**In addition to these three primary types, IdentityIQ includes other provisioning policy types for specific actions:**

*   **Enable Account:** Activates a previously disabled account on the target system.
*   **Disable Account:** Deactivates an account on the target system.
*   **Unlock Account:** Resets the locked status of an account, enabling the user to log in.
*   **Change Password:** Modifies the account's password.
*   **CreateGroup:** Creates a new group on the target system.
*   **UpdateGroup:** Updates the attributes or membership of an existing group.

**Provisioning Policies in Action**

Provisioning policies are implemented as forms. These forms determine the attributes included in provisioning requests and how their values are supplied.  For instance, when a user requests a business role requiring access to an application, IdentityIQ utilizes the corresponding provisioning policy. It pulls the required attributes from the policy and includes them in the provisioning plan. The values for these attributes can be:

*   **Manually provided:** The IdentityIQ user fills in the required information in a form.
*   **Automatically derived:** IdentityIQ calculates the values using a script or rule.
*   **Set as static values:** Predefined values are used for certain attributes.

The sources highlight an example where a provisioning policy for creating new LDAP accounts is predefined, but can be customized to meet specific business needs.

**Form Editor for Provisioning Policy Configuration**

IdentityIQ provides a Form Editor UI for configuring provisioning policies. The Form Editor allows administrators to define various settings for each field, such as:

*   **Field Name:** Must match the corresponding native attribute on the target application.
*   **Review Required:** Ensures that the field is always displayed on the form during provisioning, even if a default value is provided or calculated.

The sources note that while the Form Editor offers a user-friendly way to configure provisioning policies, advanced customization might require editing the XML definition directly.

**Provisioning Policy Ownership**

When defining provisioning policies, you can specify an owner using the `<OwnerDefinition>` element. The owner can be defined using:

*   **A literal string:** Specifies the owner's name directly.
*   **A script:** Allows dynamic determination of the owner based on specific logic.

IdentityIQ also provides special names that are translated into the appropriate identity, eliminating the need for an `<OwnerDefinition>` script:

*   **IIQParentOwner:** Represents the owner of the role or application containing the provisioning policy.
*   **IIQApplicationOwner:** Denotes the owner of the application associated with the provisioning policy.
*   **IIQRoleOwner:** Refers to the owner of the role containing the provisioning policy.

If the `<OwnerDefinition>` element is left empty (`<OwnerDefinition value=""/>`), the access requester is assigned as the owner and presented with the corresponding field.

By understanding the different types of IdentityIQ provisioning policies and how they are configured, administrators can effectively manage the process of granting and revoking access to applications and resources within their organizations.
