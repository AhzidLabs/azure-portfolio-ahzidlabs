# Project: Onboard Automator (Identities & Governance)

**Scenario:** Automate new-hire onboarding: create an Entra ID user, assign RBAC, and apply tags/locks to a Resource Group.

**Services:** Entra ID (Azure AD), RBAC, Resource Groups, Tags, Locks, (optional) Logic Apps / Automation, Key Vault.

**Why it matters:** Mirrors real helpdesk/admin work and proves governance discipline for AZ-104.

## Steps
1. Create Resource Group `RG-Onboard-Automator` (North/West Europe).
2. Create a user: **Entra ID → Users → New user** (temporary password).
3. Assign RBAC at RG scope: **Access control (IAM) → Add role assignment → Reader/Contributor** to the user.
4. Add **Tags**: `Department=HR`, `Environment=Test`.
5. Add a **Resource Lock** (Read-only) to prevent accidental changes.
6. *(Optional)* Build a **Logic App**: trigger on “New email”, create user, add to group.

## PowerShell (Cloud Shell)
```powershell
# Create user
New-AzADUser -DisplayName "John Doe" -UserPrincipalName "john.doe@<tenant>.onmicrosoft.com" -MailNickname "johndoe" -Password "P@ssw0rd123!"

# Assign role at RG scope
$rg = "RG-Onboard-Automator"
$sub = (Get-AzContext).Subscription.Id
$scope = "/subscriptions/$sub/resourceGroups/$rg"
New-AzRoleAssignment -SignInName "john.doe@<tenant>.onmicrosoft.com" -RoleDefinitionName "Reader" -Scope $scope
Evidence (Screenshots to upload later)

RG overview (name & region)

Entra ID user list (redacted)

IAM role assignment view

Tags & Locks pages

(Optional) Logic App run history

Cost

≈ £0–£0.40/month (per-run billing only; Entra ID Free = £0).
