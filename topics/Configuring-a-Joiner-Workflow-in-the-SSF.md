# Configuring a &quot;Joiner&quot; Workflow in the SSF

## Configuring a "Joiner" Workflow in the SSF

The sources provide a detailed breakdown of how to configure a "Joiner" workflow within the Services Standard Framework (SSF). The Joiner Feature is designed to handle the automated provisioning of access, often referred to as "birthright provisioning," that occurs when new employees join an organization. This automated process ensures new personnel receive the appropriate access based on their role and attributes.

Here is a comprehensive step-by-step guide to configuring the Joiner workflow using the SSF:

**1. Configure Target Properties**

*   The `ssf.target.properties` file serves as a template for managing the Joiner feature.
*   Begin by locating the "Joiner Feature Properties" section in this file and transferring all entries to the `target.properties` file for your specific environment. You can automate this step using the SSD Deployer tool, which simplifies environment setup.
*   Set the property `SP_JOINER_IS_DISABLED` to `false` to enable the feature.
*   Adjust the remaining attributes to `true` or `false` based on your requirements and the guidance provided in the comments within the file. These attributes control aspects such as workflow tracing and email notifications.

**2. Configure Trigger Attributes**

*   Trigger attributes dictate the conditions under which the Joiner workflow will be initiated for a given identity. These attributes are defined within the `SPCONF Joiner Mappings Custom` object.
*   **Specify the Trigger Type:** Choose how the system determines if an identity qualifies as a "Joiner." You have two options:
    *   **Selector:** Use an `IdentitySelector` to define a set of attribute values that identify a joiner. For instance, you might trigger the workflow for identities with an active status and a null joiner date.
    *   **Custom Rule:** Utilize a custom rule or rule library method to evaluate the identity and return `true` if the Joiner event should be executed. The `SPCONF Joiner Mappings Custom` object provides a default rule library method (`isJoinerCustomTriggerRule`), which you can customize with your specific logic.

**3. Determine Birthright Assignment Type**

*   The method of assigning access to new joiners can vary based on organizational needs. The `Birthright Assignment Type` attribute within the `SPCONF Joiner Mappings Custom` object controls how the provisioning plan is constructed during the "Build Plan" workflow step.
*   **Select an assignment type from the following options:**
    *   **Dynamic Roles:** Leverages the Role Assignment Framework to dynamically assign roles to identities based on predefined rules and criteria.
    *   **Default Roles:** Assigns a fixed list of roles, defined in the `Default Assignments` entry of the custom mapping object, to all new joiners.
    *   **Default Applications:** Grants accounts on a predefined set of applications, also specified in the `Default Assignments` entry, to each joiner.
    *   **Custom Rule:** Employs a custom rule, named in the `Birthright Assignment Custom Rule` entry, to build the provisioning plan and determine access assignments.

**4. Configure Assignment Details**

*   Based on the chosen `Birthright Assignment Type`, you'll need to configure the specific details of how access is assigned.
*   For **Dynamic Roles,** configure the Role Assignment Framework as outlined in the relevant section of the documentation.
*   For **Default Roles or Default Applications**, list the roles or applications in the `Default Assignments` entry of the `SPCONF Joiner Mappings Custom` object.
*   For **Custom Rule,** provide the rule name in the `Plan Construction Custom Rule` entry. The custom mapping object includes a default rule library method (`buildCustomJoinerPlan`) that you can customize for your requirements.  This rule receives an `Identity` object as input and must return a `ProvisioningPlan` object containing the desired access assignments.

**5. Configure Workflow Hooks**

*   The Joiner workflow incorporates various hooks that allow you to introduce custom logic and extend its functionality. These hooks are typically implemented as methods within the `SPCONF Joiner Rule Library`.
*   **Examples of available hooks:**
    *   `getjoinerRequestTypeRule`: Defines the "request type" string, used by the Approval Framework to determine the appropriate approval process.
    *   `joinerBeforePlanRule`: Enables custom actions prior to the provisioning plan creation. The provided method offers a template for retrieving and modifying workflow variables like `identityModel` and `spExtAttrs`.
    *   `joinerNoRequestRule`: Executes custom logic when no provisioning plan is required. This hook can be used to set extended attributes or perform other actions.
    *   `joinerBeforeProvisionRule`: Facilitates customization before provisioning begins.
    *   `joinerAfterProvisionRule`: Allows actions to be taken after the provisioning process completes. For example, it could be used to set the joiner date.

**6. Deploy the Feature**

*   Integrate the customizable files from the "Configure" folder of the Joiner Feature, along with those from any dependent frameworks, into the SSB `/config` folder. The SSD Deployer tool can automate this process.
*   The `/config` folder is typically organized into subfolders based on object types, so ensure the files are placed appropriately.
*   Deploy the artifacts using the SSB deployment process, which will import the necessary configurations and code into your IdentityIQ environment.

By following these steps, you can effectively configure the Joiner workflow within the SSF to automate the provisioning of access for new employees in your organization. The SSF provides a structured and flexible framework, enabling you to tailor the workflow to meet your specific requirements while leveraging pre-built components and best practices.
