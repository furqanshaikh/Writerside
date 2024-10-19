# Dynamically Changing Email Templates with the Enhanced Email Notifier

## Dynamically Changing Email Templates with the Enhanced Email Notifier

The Enhanced Email Notifier tool expands upon IdentityIQ's standard email notification capabilities, introducing features that enhance flexibility and functionality. One notable feature is the ability to **dynamically modify the email template used to render an email before it's sent**. This capability allows for tailoring email content based on specific conditions or recipient attributes, making notifications more informative and relevant.

The Enhanced Email Notifier achieves this dynamic template switching through two primary mechanisms:

1.  **Dynamic Email Rule Name:**

    *   This mechanism relies on a configurable rule, specified by the `dynamicEmailRuleName` key in the Notifier's configuration object.
    *   When an email notification is triggered, the Enhanced Email Notifier executes this rule. The rule receives several inputs, including the original email template, email options (metadata used to render the email), SailPoint context, email address, and the identity associated with the email.
    *   Based on these inputs, the rule can evaluate conditions and determine if a different template is more appropriate. The rule's output must be a string containing the name of the new email template. If the specified template exists, it will be used to render the email instead of the original template. If the template doesn't exist, the original template is used.
2.  **Dynamic Email Identity Attribute:**

    *   This approach uses an identity attribute to dynamically augment the template name. You configure this by specifying the attribute name in the `dynamicEmailIdentityAttribute` key within the Notifier's configuration object.
    *   When an email is being prepared, the Notifier appends an underscore ("\_") followed by the value of the specified identity attribute to the original template name. For instance, if the template name is "Work Item Assignment" and the identity attribute is "language" with a value of "GB," the Notifier will search for a template named "Work Item Assignment\_GB".
    *   This method is particularly useful for scenarios like multi-language email support, where you can store the user's language preference in an identity attribute and have the Notifier automatically select the appropriate language template. If the augmented template name isn't found, the system falls back to the original template.

**Order of Operations:**

The Enhanced Email Notifier executes these dynamic template selection processes in a specific order:

1.  **Dynamic Email Rule Name:** The system first attempts to apply the rule specified by `dynamicEmailRuleName` to potentially change the template.
2.  **Dynamic Email Identity Attribute:** If the rule doesn't change the template name, the Notifier proceeds to augment the template name based on the `dynamicEmailIdentityAttribute` setting.

**Use Case Example:**

Consider a scenario where you want to send different access request notifications to internal employees and external contractors. You could configure a dynamic email rule that checks the identity's "userType" attribute. If the value is "Employee," it returns the template "Access Request Notification - Internal," and if the value is "Contractor," it returns "Access Request Notification - External." This allows you to tailor the email content and messaging based on the recipient's internal or external status.
