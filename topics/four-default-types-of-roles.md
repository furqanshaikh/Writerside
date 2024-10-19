# four default types of roles

Here are the four default types of roles configured in IdentityIQ, as described in the sources:

*   **Organizational Roles:** These roles are primarily used to structure and organize the role hierarchy within IdentityIQ's user interface, particularly in the Role Modeler. They don't inherently possess any functional capabilities beyond establishing a hierarchical framework for managing roles. You can design the hierarchical structure of organizational roles in a variety of ways to suit your organizational needs. For example, you could structure them based on departments, business units, or geographical locations.
*   **Business Roles:** Business roles in IdentityIQ represent logical groupings of users based on their job functions, responsibilities, or positions within the organization. These roles abstract away the technical details of access permissions and present a more user-friendly and understandable way to manage access. For example, a "Marketing Manager" business role might encompass various entitlements related to marketing systems and resources. IT roles are often linked to business roles to map actual access permissions to these defined job functions.
*   **IT Roles:** These roles focus on modeling the technical access permissions required to perform specific tasks or functions within applications or systems. IT roles typically group together individual entitlements into more meaningful units that align with how access is granted and managed within IT systems. For instance, an "Account Payable Clerk" IT role might include entitlements to access the accounting system and perform specific financial transactions.
*   **Entitlement Roles:** Entitlement roles were originally designed to represent a single entitlement on a specific application. However, the sources note that these roles are now primarily maintained for backward compatibility with older versions of IdentityIQ. It's generally recommended to avoid using entitlement roles in current or new IdentityIQ implementations.

**Custom Roles**

Beyond these four default role types, IdentityIQ allows you to create custom role types to accommodate unique organizational structures or access models. These custom roles can be tailored to function differently from the default types to meet specific business requirements.

**Key Concepts Related to Roles in IdentityIQ**

*   **Role Management:** IdentityIQ provides a comprehensive set of features for managing roles, including creating, editing, deleting, assigning, and monitoring roles. These features aim to help organizations implement robust role-based access control models and streamline access governance processes.
*   **Two-Tier Role Model:** IdentityIQ's default role model uses a two-tier structure that links IT roles to business roles. This model allows for a clear mapping between the technical details of access permissions (represented by IT roles) and the business functions and job titles (represented by business roles).
*   **Role Inheritance:** IdentityIQ supports role inheritance, allowing you to create hierarchical relationships between roles. When a role inherits from a parent role, it automatically acquires the entitlements and permissions associated with the parent role.
*   **Role Assignment:** Roles can be assigned to identities in IdentityIQ through various methods:
    *   **Manual Assignment:** An administrator can directly assign roles to identities.
    *   **Role Assignment Rules:** Automated rules can assign roles to identities based on specific criteria, such as job title or department.
    *   **Role Detection:** IdentityIQ can automatically detect IT roles for identities based on their existing entitlements.

**Role Management Tools in IdentityIQ**

*   **Role Viewer:** The Role Viewer interface allows you to view, create, edit, and delete roles. It also provides detailed information about each role, including its type, owner, scope, and associated entitlements.
*   **Role Editor:** The Role Editor provides a more in-depth view of a role's properties and configurations. You can use it to define the role's name, display name, type, owner, scope, description, and other attributes.
*   **Role Mining:** IdentityIQ includes role mining capabilities that analyze existing access patterns and suggest potential roles. You can use role mining to discover both business roles based on identity attributes (e.g., department, job title) and IT roles based on entitlements.
*   **Entitlement Analysis:**  This feature helps you identify patterns in entitlements and create roles based on logical groupings of access permissions. Entitlement analysis can streamline role creation by automating the process of analyzing and grouping entitlements.
*   **Role Composition Certification:**  This type of certification focuses on reviewing the access permissions included within a role. Role owners or designated reviewers can assess the appropriateness of the entitlements within a role and make necessary adjustments to ensure its accuracy and relevance.

By understanding these default role types and associated concepts, you can effectively leverage IdentityIQ's role management capabilities to implement a robust role-based access control model that aligns with your organization's structure and business processes. 
