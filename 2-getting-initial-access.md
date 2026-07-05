
## 2. Initial Access & Authentication Validation

**Goal:** Establish an authorized session in-scope and confirm what it can actually reach.

1. Authenticate with approved/provided credentials — `Connect-AzAccount`, `Connect-MsolService`
2. Import a pre-authorized context if the engagement provides one — `Import-AzContext`
3. Persist the session for the engagement window — `Save-AzContext`
4. Validate the access scope matches what was authorized (no more, no less)
5. Enumerate current role assignments — `Get-AzRoleAssignment`
6. Identify baseline privilege level for the tested identity
7. Switch/validate access across in-scope subscriptions — `Select-AzSubscription`

> Any MFA-bypass or stolen-token simulation must be pre-approved in writing and performed only against test identities, never live user sessions, per the engagement's ethical constraints.
