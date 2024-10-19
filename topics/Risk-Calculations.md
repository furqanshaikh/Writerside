# Risk Calculations

Here are three ways to define how IdentityIQ calculates base access risks for roles, entitlements, and policy violations, based on the sources:

*   **Literal Values:** You can directly specify a literal risk score for each role, entitlement, and policy violation. This approach involves manually assigning a numerical value to represent the inherent risk associated with each access element. For example, you might assign a higher risk score to roles that grant access to sensitive financial systems compared to roles with access to less critical resources. Similarly, entitlements that allow for data modification might receive a higher risk score than those with read-only permissions.

    *   Source states, "**Literal – value is based on the information you provide**". This statement indicates that you can input specific values to determine the risk level.
*   **Rules:** IdentityIQ allows you to create rules that define how risk scores are calculated. These rules can incorporate various factors and conditions to determine the risk level. For example, a rule might assign a higher risk score to roles that have a specific combination of entitlements or to entitlements that grant access to certain applications. You can use rules to implement more complex and dynamic risk scoring logic based on your organization's specific requirements.

    *   Source states, "**Rule – value is based on a specified rule**."
    *   Source provides an example of a rule configuration for policy violations: "Enter a custom XML database query to define identities for this rule."
    *   Source further explains, "Field where code is input. IdentityIQ recognizes BeanShell programing language. You can edit code from an existing rule or create a new one from scratch."
*   **Scripts:** Similar to rules, scripts offer a more customizable approach to defining risk scores. Scripts use programming code to calculate risk based on defined logic and criteria. You can use scripts to implement sophisticated risk assessments that consider multiple variables and external data sources.

    *   Source states, "**Script – value is determined by the execution of a script**."
    *   Source also mentions the use of scripts for policy violations: "Enter a custom script to define the rule. Scripts are similar to rules, but the source is stored with the policy and can be edited from this page." This statement suggests that you can tailor scripts to meet specific policy requirements.

**Factors Influencing Base Access Risk**

*   **Sensitivity of Data:** The sensitivity of the data accessed plays a significant role in determining risk. Access to highly confidential information, such as financial records or personal data, typically warrants a higher risk score.
*   **Level of Access:** The level of access granted also influences risk. Entitlements that allow for data modification or system administration privileges pose a higher risk than read-only or limited access permissions.
*   **Application Criticality:** The criticality of the application or system being accessed is a factor. Access to mission-critical applications or systems that could impact business operations significantly if compromised would likely have a higher risk score.

**Key Concepts Related to Risk Scoring in IdentityIQ**

*   **Base Risk Score:** This score reflects the inherent risk associated with a particular role, entitlement, or policy violation without considering any compensating controls or mitigating factors.
*   **Compensated Risk Score:** This score adjusts the base risk score by factoring in compensating controls, such as multi-factor authentication or separation of duties policies.
*   **Composite Risk Score:** The composite risk score aggregates the compensated risk scores from various components, including roles, entitlements, and policy violations, to provide an overall risk assessment for an identity or application.

By understanding these methods for defining base access risks and the factors that contribute to risk assessments, you can effectively configure IdentityIQ to align with your organization's risk tolerance and security policies. 
