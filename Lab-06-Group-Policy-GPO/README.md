# Lab 06 — Group Policy Management and Troubleshooting

## Objective

Configure, deploy, verify, and troubleshoot Group Policy Objects (GPOs) in a Windows Server Active Directory environment.

## Lab Environment

- **Hypervisor:** UTM
- **Server OS:** Windows Server 2022
- **Client OS:** Windows 10/11
- **Domain:** corp.local
- **Domain Controller:** SERVER01.corp.local
- **Directory Service:** Active Directory Domain Services (AD DS)
- **Tools:** Group Policy Management Console (GPMC), Active Directory Users and Computers (ADUC), Command Prompt

## Exercises Completed

### Exercise 1 — Explore Group Policy Management

- Opened Group Policy Management Console.
- Explored the Active Directory domain structure.
- Identified Default Domain Policy and Default Domain Controllers Policy.
- Reviewed domain password policy settings.
- Verified that the minimum password length was configured to 7 characters.

### Exercise 2 — Create and Link a GPO

- Created a new Organizational Unit (OU) named `Test-Users`.
- Created a Group Policy Object named `Restrict-Control-Panel`.
- Linked the GPO to the `Test-Users` OU.
- Configured the GPO scope to target users within the OU.

### Exercise 3 — Configure User Restrictions

Configured the following Group Policy setting:

`User Configuration → Policies → Administrative Templates → Control Panel → Prohibit access to Control Panel and PC settings`

- Set the policy to `Enabled`.
- Configured a user-based restriction to prevent access to Control Panel and Windows Settings.

### Exercise 4 — Apply and Verify Group Policy

- Created a domain user named `testuser1` inside the `Test-Users` OU.
- Signed in to a domain-joined Windows client using the test account.
- Forced Group Policy updates using:

`gpupdate /force`

- Verified that access to Control Panel was successfully blocked.
- Used the following command to inspect applied policies:

`gpresult /r`

- Confirmed that `Restrict-Control-Panel` appeared under Applied Group Policy Objects while the restriction was active.

### Exercise 5 — Group Policy Troubleshooting

- Identified the GPO responsible for restricting Control Panel access.
- Changed the policy setting from `Enabled` to `Not Configured`.
- Refreshed Group Policy on the Windows client.
- Verified that Control Panel access was restored.
- Executed `gpresult /scope user /r` to inspect the final policy state.
- Observed that `Restrict-Control-Panel` appeared under filtered-out GPOs with the status `Not Applied (Unknown Reason)`.
- Confirmed that the restriction was no longer active.

## Screenshots

### 1. GPO Linked to Organizational Unit

![GPO Linked](screenshots/01-gpo-linked.png)

Shows the `Restrict-Control-Panel` GPO linked to the `Test-Users` Organizational Unit in Group Policy Management.

### 2. Test User in Active Directory

![Test User](screenshots/02-test-user.png)

Shows the domain user `testuser1` created inside the `Test-Users` OU using Active Directory Users and Computers.

### 3. Group Policy Configuration

![Policy Configuration](screenshots/03-policy-configuration.png)

Shows the Control Panel restriction policy configuration in Group Policy Management Editor. The final setting is `Not Configured` after troubleshooting.

### 4. Group Policy Verification After Troubleshooting

![GPO Verification](screenshots/04-gpresult-after-troubleshooting.png)

Shows the results of `gpresult /scope user /r` after troubleshooting.

The `Restrict-Control-Panel` GPO is listed under filtered-out policies with the status `Not Applied (Unknown Reason)`. The policy restriction had previously been changed from `Enabled` to `Not Configured`.

This screenshot documents the final Group Policy processing state after the restriction was removed.

### 5. Control Panel Access Restored

![Access Restored](screenshots/05-access-restored.png)

Shows that Control Panel is accessible again after modifying the Group Policy setting and refreshing policies on the Windows client.

## Verification Results

| Test | Result |
|---|---|
| GPO created and linked to OU | Passed |
| Test user created in target OU | Passed |
| GPO applied to domain user | Passed |
| Control Panel access restricted | Passed |
| GPO verified using gpresult | Passed |
| Policy restriction removed | Passed |
| Control Panel access restored | Passed |

## Key Concepts Learned

- Group Policy Objects (GPOs)
- Organizational Units (OUs)
- GPO linking and scope
- User Configuration vs. Computer Configuration
- Administrative Templates
- Group Policy refresh using `gpupdate /force`
- Group Policy verification using `gpresult /r`
- GPO filtering and troubleshooting
- Enabled, Disabled, and Not Configured policy states

## Conclusion

Successfully configured, deployed, verified, and troubleshot a user-based Group Policy Object in an Active Directory environment.

Demonstrated practical experience with GPO creation, Organizational Unit management, user restrictions, policy verification, and troubleshooting.

Successfully restored Control Panel access by modifying the configured restriction and refreshing Group Policy on the domain-joined Windows client.
