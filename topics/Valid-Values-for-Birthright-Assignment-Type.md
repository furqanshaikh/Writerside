# Valid Values for Birthright Assignment Type

## Valid Values for Birthright Assignment Type

The **Birthright Assignment Type** entry in the **SPCONF Joiner Mappings Custom object** dictates how the provisioning plan is built within the *Build Plan* step of the *Joiner* workflow. You can choose from four valid values for this attribute:

*   **Dynamic Roles:** This option leverages the *Role Assignment Framework* to dynamically determine and assign roles to the new joiner identity. It's important to note that using this option necessitates the *Role Assignment Framework* being configured and operational in your IdentityIQ environment.
*   **Default Roles:** This option assigns a predetermined set of roles to the joiner identity. These roles are listed within the **Default Assignments** entry of the SPCONF Joiner Mappings Custom object.
*   **Default Applications:** This option focuses on provisioning accounts for the joiner identity on a pre-defined list of applications. Similar to "Default Roles," the applications are specified within the **Default Assignments** entry of the SPCONF Joiner Mappings Custom object.
*   **Custom Rule:** This option offers the greatest flexibility, enabling you to define custom logic for building the provisioning plan. This logic is implemented in a rule specified in the **Birthright Assignment Custom Rule** entry of the SPCONF Joiner Mappings Custom object. The default rule for this entry is the **buildCustomJoinerPlan** method, which is part of the SPCONF Joiner Rule Library. It's recommended to leverage this method and incorporate your custom logic within it. This rule (or method) must take an *Identity* object as input and return a *ProvisioningPlan* object.

The SPCONF Joiner Mappings Custom object, mentioned in the sources as "SPCONF\_Joiner\_Mappings\_Custom.xml", plays a central role in configuring the *Joiner* feature. It contains settings that determine when the workflow runs (trigger conditions), the method used for assigning initial access ("Birthright Assignment Type"), and other parameters. This object is customized to meet each organization's specific IAM needs.
