# Default Rule for Trigger Custom Rule in SPCONF Joiner Mappings

## Default Rule for Trigger Custom Rule in SPCONF Joiner Mappings

The **default rule** used for a **Trigger Custom Rule** in the **SPCONF Joiner Mappings Custom object** is the **isJoinerCustomTriggerRule** method found in the **SPCONF Joiner Rule Library**. This information is relevant when setting up the *Joiner feature*, one of the features offered by the SailPoint Services Standard Framework (SSF).

The SSF offers a collection of pre-built frameworks and features designed to simplify and expedite SailPoint IdentityIQ implementations. These features aim to address typical Identity and Access Management (IAM) requirements through reusable components. For instance, the Joiner feature automates the provisioning of access for new employees, often referred to as "birthright provisioning."

### Joiner Feature Trigger Configuration

The Joiner feature utilizes a Lifecycle Event (LCE) trigger, allowing for the initiation of workflows based on changes in identity data. The trigger is flexible and offers multiple methods for determining when to execute the Joiner workflow. These trigger options are defined within the SPCONF Joiner Mappings Custom object, which acts as a central configuration hub for the Joiner feature.

Within this custom object, the "Trigger Type" entry determines the mechanism used to identify "joiner" identities. The available options are:

*   **Selector:** This option utilizes an IdentitySelector to define a specific set of attributes and their values that characterize a "joiner" identity. The Joiner trigger will compare an identity against the defined criteria in the IdentitySelector, triggering the workflow if a match is found.
*   **Custom Rule:** This option allows for more complex and customized logic in determining "joiner" identities. It uses a custom rule, typically a rule library method, to evaluate the identity and decide whether to trigger the workflow.

### The Importance of the isJoinerCustomTriggerRule Method

When the "Trigger Type" is set to "Custom Rule," the **Trigger Custom Rule** entry in the SPCONF Joiner Mappings Custom object specifies the rule or rule library method to be executed. **By default, this entry points to the isJoinerCustomTriggerRule method within the SPCONF Joiner Rule Library**.

This method offers a pre-built framework for custom "joiner" identification logic. While it may initially be empty or contain basic template logic, you can modify this method to incorporate your organization's specific requirements for defining a "joiner."

By using this pre-defined rule library method, you can centralize your custom logic within the SPCONF Joiner Rule Library. This promotes better organization, maintainability, and reduces the need to create and manage separate custom rules for each individual Joiner trigger scenario.
