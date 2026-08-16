# Azure RBAC Lab

## Objective

Practice Azure Role-Based Access Control (RBAC) using the Azure Portal and understand how role assignments, scope, inheritance, and least privilege work.

## Concepts Practiced

- Azure RBAC
- Microsoft Entra ID integration
- Role assignments
- Security principals
- Role definitions
- Scope and inheritance
- Least privilege
- Access control (IAM)

## RBAC Model

Azure RBAC can be understood as:

**Who + What + Where**

- **Who:** User, group, service principal, or managed identity
- **What:** Role definition containing permissions
- **Where:** Management group, subscription, resource group, or resource

## Hands-On Exercise

Assigned the **Virtual Machine Contributor** role to a test user at the **resource group** scope.

### Configuration

- **Security principal:** Chris Green
- **Role:** Virtual Machine Contributor
- **Scope:** Resource group
- **Resource group:** Sean-Labs

The assignment was verified in **Access control (IAM)** and then removed to complete the access-removal portion of the exercise.

## Key Takeaways

- Azure RBAC controls authorization to Azure resources.
- Permissions assigned at a parent scope can be inherited by child resources.
- Contributor can manage resources but cannot assign RBAC roles.
- Owner has full access and can assign roles.
- Least privilege means granting only the permissions required at the smallest practical scope.
- Microsoft Entra ID provides the identity; Azure RBAC determines what that identity can do.

## Skills Demonstrated

- Azure Portal
- Azure RBAC
- Microsoft Entra ID
- IAM
- Role-based access control
- Least privilege
- Azure resource governance
