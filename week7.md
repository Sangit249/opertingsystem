

# Phase 7: Security Audit and System Evaluation

## 1\. Infrastructure Security Assessment

The goal of this audit was to verify the effectiveness of the security controls implemented throughout the project. The assessment combined automated scanning with manual verification of access controls.

### 1.1 Automated Audit: Lynis

Lynis was used to perform a deep system scan to calculate a **Hardening Index**.

- **Command:** sudo lynis audit system
- **Lynis Scores:**
  - **Initial Score:** 62 (Baseline after standard install)
  - **Final Score:** **84** (After remediation and hardening)

### Key Remediation Actions:

- Implemented password aging limits in /etc/login.defs.
- Hardened the SSH configuration by disabling root login.
- Installed a malware scanner (chkrootkit).

## 2\. Network Security Testing (Nmap)

I conducted an external network scan from the **Workstation** to ensure the firewall (UFW) was correctly filtering traffic.

- **Command:** nmap -sV -p- -T4 \[Server_IP\]
- Results:

## 3\. SSH Security & Access Control Verification

I manually verified that the identity and access management (IAM) policies were active.

- **SSH Verification:** Running grep "PermitRootLogin" /etc/ssh/sshd_config confirms the value is no.
- **Access Control:** Attempting to log in as root via SSH resulted in a "Permission Denied" error, confirming that only the sangit_admin user can access the system.
- **SUID Check:** I ran find / -perm -4000 -type f to ensure no new or suspicious "Set User ID" binaries were present that could lead to privilege escalation.

## 4\. Service Inventory & Justification

As part of the audit, I reviewed all active services to ensure no unnecessary processes were running.

| **Service Name** | **Status** | **Justification** |
| --- | --- | --- |
| sshd.service | Running | Essential for remote CLI management. |
| nginx.service | Running | Serves the web application to end-users. |
| ufw.service | Running | Manages the system's packet filtering (Firewall). |
| systemd-journald | Running | Critical for logging and audit trails. |

## 5\. Remaining Risk Assessment

Despite a high Lynis score, the following residual risks exist:

- **Application Vulnerabilities:** While the OS is hardened, vulnerabilities within the web application code itself remain a risk.
- **Brute Force:** Although root login is disabled, the SSH port is standard (22). **Mitigation:** Implementing fail2ban is recommended for future phases.
- **Physical/Host Access:** As a VM, security is dependent on the hypervisor's integrity.

## 6. Conclusion

The audit confirms that the system is significantly more secure than its original state. The jump in the Lynis Hardening Index from 62 to 84, combined with the "Filtered" status of non-essential ports in Nmap, proves that the defense-in-depth strategy was successfully implemented.
