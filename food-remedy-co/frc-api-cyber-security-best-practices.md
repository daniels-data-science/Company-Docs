# Proposal Documentation: CYBER SECURITY BEST PRACTICES

**Abin Abraham Jacob**
**21st August, 2023**

## Introduction - Security Auditing

A security audit is a systematic process that calculates and checks an organization’s or a system's security posture, practices, and controls to detect vulnerabilities, assess risks, and ensure compliance with policies, books, and security standards. This involves a comprehensive review of security configurations, processes, procedures, and technologies to identify weaknesses and areas for improvement. The goal of a security audit is to improve the overall security of the organization and reduce the possibility of a security breach or incident. Security auditing can be conducted internally by an organization's own security team or externally by independent auditors. It may involve automated tools for vulnerability scanning, penetration testing, and log analysis, as well as manual assessments by experts. The results of a security audit are typically documented in an audit report, which outlines findings, risks, and recommendations for improving security measures.

## Key Aspects of Security Auditing

- **Risk Assessment:** Identifying potential risks and threats to the organization's assets, data, and infrastructure.
- **Review of Policies and Procedures:** Evaluating the organization's security policies, guidelines, and procedures to ensure they are comprehensive and up-to-date.
- **Access Controls:** Assessing the effectiveness of access controls and permissions to prevent unauthorized access to sensitive data or systems.
- **Data Protection:** Examining data storage, encryption, and handling practices to safeguard sensitive information.
- **Network Security:** Evaluating firewalls, intrusion detection/prevention systems, and network segmentation to prevent unauthorized access.
- **Application Security:** Assessing the security of applications, including code quality, vulnerability assessments, and secure coding practices.
- **Configuration Management:** Reviewing system and network configurations to ensure they align with security best practices.
- **Physical Security:** Reviewing physical access controls to data centers and other critical facilities.
- **Incident Response:** Evaluating the organization's incident response plan and its readiness to address security incidents.
- **Compliance:** Ensuring compliance with industry regulations and legal requirements.

## Accidental Exposure using OSINT (Open Source Intelligence)

### 1. GitHub Repository Scrutiny:

- Attackers scan GitHub repositories for commits containing keywords like "password," "key," or "token."
- Tools like TruffleHog and GitRob can search repositories for sensitive information.
- Example: An attacker finds a commit in a public repository with a plaintext AWS access key.

### 2. Code Sharing Platforms:

- Developers sometimes share code snippets containing credentials on platforms like Pastebin or Gist.
- Attackers use Google Dorks (advanced search queries) to find publicly shared credentials.
- Example: A developer inadvertently shares a Python script with hardcoded API keys on Pastebin.

### OSINT Tools

- **TruffleHog:** Searches for high entropy strings and keywords in Git repositories.
- **GitRob:** Scans GitHub repositories for exposed sensitive information.
- **Google Dorks:** Custom search queries to find specific information using Google's search engine.

### Scraping Tools

- **Web Scrapers:** Tools like Scrapy or Beautiful Soup automate data extraction from websites.
- **Malicious Bots:** Attackers deploy malicious bots to scrape and collect data from websites.

### Advanced Google Search

Advanced Google search techniques can help you identify instances of security hardcoded credentials online.

- **Identify Keywords:** Start by identifying relevant keywords that are commonly used in hardcoded credentials. These could include terms like "password," "secret," "API key," "access token," etc.
- **Use Quotation Marks:** Wrap your search terms in quotation marks to search for exact phrases. For example, search for "password=12345" or "API key=abcdef".
- **Exclude Common Pages:** To avoid common pages like documentation and tutorials, you can exclude specific domains from your search. For example, -site:github.com will exclude results from GitHub.
- **File Type Search:** Search for specific file types that often contain configuration files with hardcoded credentials. Use the filetype: operator, such as filetype:xml password.
- **Inurl Operator:** Use the inurl: operator to search for specific terms in the URL of a page. For example, inurl:config secret.
- **Wildcard Operator:** Use the * wildcard to capture variations of a term. For instance, "API key=*" will search for different API key values.
- **Intitle Operator:** Use the intitle: operator to find pages with specific terms in their title. For example, intitle:"login credentials".
- **Boolean Operators:** Combine operators like AND, OR, and NOT to refine your search. For example, password OR "API key" NOT tutorial.
- **Search Specific Domains:** Target specific domains that might be relevant to your search, like specific websites or forums where developers discuss code.

**Example:** "password=12345" OR "API key=abcdef" -site:github.com -site:stackoverflow.com filetype:xml

Additionally, you might consider using dedicated tools and platforms designed for searching for leaked or exposed credentials on the internet, as they can provide more focused and comprehensive results. Examples of such tools include Shodan, Censys, and Have I Been Pwned.

### Points to Keep in Mind

1. **Avoid Hardcoding Credentials:**

- Use environment variables or secure credential stores instead of hardcoding keys.
- Implement secure secret management solutions like HashiCorp Vault.

2. **Regular Scanning:**

- Regularly scan code repositories and web platforms for sensitive data.
- Use automated tools like GitGuardian to monitor repositories for exposed credentials.

3. **Gitignore and .gitkeep:**

- Properly configure your .gitignore file to exclude sensitive files from version control.
- Use .gitkeep files to ensure empty directories are not accidentally committed.

4. **Security Awareness:**

- Train developers and team members about secure coding practices and the risks of accidental exposure.

## Mismanagement of IAM Policies and Security Misconfigurations

### 1. Overly Permissive IAM Policies:

- Scenario: Assigning broad permissions to users or roles, allowing unintended access to sensitive resources.
- Risk: Unauthorized access, data leakage, and potential compromise of critical resources.

### 2. Lack of Principle of Least Privilege (PoLP):

- Scenario: Assigning excessive permissions beyond what's necessary for a user's role.
- Risk: Increased attack surface, potential for privilege escalation, and data breaches.

### 3. Unrestricted External Access:

- Scenario: Allowing open access to resources from any IP address.
- Risk: Exposure to attacks from malicious actors, such as DDoS or unauthorized data exfiltration.

### 4. Inadequate Logging and Monitoring:

- Scenario: Failing to set up proper logging and monitoring for IAM actions.
- Risk: Difficulty in detecting unauthorized or suspicious activities, hindering incident response.

### 5. Unused Credentials and Access Keys:

- Scenario: Leaving unused IAM users, roles, or access keys active.
- Risk: Increased attack surface, potential for unauthorized access, and resource wastage.

### Managing IAM Policies and Security Best Practices

1. **Principle of Least Privilege (PoLP):**

- Practice: Assign minimal permissions required for each user or role.
- Benefit: Reduces potential damage in case of a compromise and limits lateral movement.

2. **Regularly Review and Update Policies:**

- Practice: Conduct periodic reviews of IAM policies and permissions.
- Benefit: Ensures that permissions are aligned with users' roles and responsibilities.

3. **Use Managed Policies:**

- Practice: Utilize AWS-managed policies or create custom policies based on the principle of least privilege.
- Benefit: Ensures that policies follow best practices and are regularly updated by AWS.

4. **Implement Multi-Factor Authentication (MFA):**

- Practice: Enable MFA for IAM users to add an additional layer of security.
- Benefit: Reduces the risk of unauthorized access even if credentials are compromised.

5. **Centralized Access Control:**

- Practice: Use AWS Identity and Access Management (IAM) to centrally manage user access.
- Benefit: Provides a unified way to manage permissions across AWS services.

## Inculcating Good Security Practices into the Project

1. **Security Training and Awareness:**

- Conduct regular security training for developers, administrators, and all team members.
- Emphasize the importance of IAM best practices and common security misconfigurations.

2. **Automated Tools and Testing:**

- Integrate automated security testing tools into the CI/CD pipeline.
- Tools like AWS Config, AWS Trusted Advisor, or third-party solutions can help identify security misconfigurations.

3. **Code Reviews and Peer Feedback:**

- Implement a code review process that includes security checks.
- Encourage developers to review each other's code for IAM policy-related issues.

4. **Documentation and Guidelines:**

- Create comprehensive documentation on IAM best practices and security considerations.
- Make these documents easily accessible to the development team.

5. **Regular Auditing and Monitoring:**

- Set up regular audits and monitoring for IAM policies and access.
- Respond promptly to any detected security misconfigurations.

6. **Incident Response Plan:**

- Develop a clear incident response plan to address security incidents related to IAM policies.
- Ensure that all team members understand their roles and responsibilities in case of a security breach.

By incorporating these practices into the project's development lifecycle and fostering a culture of security awareness, you can significantly reduce the risks associated with IAM policy mismanagement and security misconfigurations.

## GitHub Security Auditing

### 1. Introduction

A security audit of GitHub repositories and accounts is vital to ensure the protection of sensitive data, prevent unauthorized access, and mitigate potential security risks. This guide outlines a step-by-step process for conducting a thorough security audit.

### 2. Scope of Audit

The security audit will encompass the following aspects:
- Access control and permissions for repositories and users.
- Detection and prevention of sensitive data exposure.
- Integration and effectiveness of automated security scanning.
- Monitoring of audit logs and suspicious activities.

### 3. Access Control and Permissions

#### Steps:
1. Repository Access Review:
   - Evaluate the access control settings of each repository.
   - Review collaborators, teams, and their permissions.
2. Principle of Least Privilege (PoLP):
   - Assess whether permissions are aligned with job roles.
   - Identify and rectify overprivileged accounts.

#### Recommendations:
- Enforce two-factor authentication (2FA) for all collaborators.
- Regularly review and adjust repository permissions.

### 4. Sensitive Data Exposure

#### Steps:
- Scanning for Exposed Credentials
   - Utilize tools like GitRob to scan for exposed credentials.
   - Search for keywords like "password," "secret," and "token."
- Review Configuration Files
   - Examine configuration files for hardcoded secrets.
   - Look for sensitive data in files like .env or .config.

#### Recommendations:
- Implement GitHub's secret scanning to prevent sensitive data leakage.
- Educate developers on the risks of exposing sensitive information.

### 5. Automated Security Scanning

#### Steps:
1. Enable GitHub Security Alerts:
   - Enable automated security alerts for repositories.
   - Configure notifications for vulnerabilities in dependencies.
2. Integrate Third-Party Scanning Tools:
   - Integrate third-party security scanning tools like Snyk or Travis CI.
   - Set up automated vulnerability scans for each repository.

#### Recommendations:
- Regularly review and act upon automated security alerts.
- Include automated security scanning as part of the CI/CD pipeline.

### 6. Audit Logs and Monitoring

#### Steps:
1. Review GitHub Audit Logs:
   - Examine audit logs for suspicious activities.
   - Monitor changes to repository settings and permissions.
2. User Activity Analysis:
   - Analyze the activity of collaborators and users.
   - Look for unusual access patterns.

#### Recommendations:
- Set up notifications for unusual account access or activities.
- Conduct regular reviews of audit logs to detect unauthorized actions.

### 7. Integrating Security Practices

#### Steps:
1. Secure Coding Guidelines:
   - Establish and communicate secure coding practices.
   - Provide guidelines for handling credentials and sensitive data.
2. Incident Response Plan:
   - Develop an incident response plan to address security breaches.
   - Define roles and responsibilities in case of a security incident.

#### Recommendations:
- Conduct regular security training sessions for developers.
- Foster a culture of security awareness within the organization.

## Trello Security Configuration Audit

### 1. Introduction

A security audit of a Trello account is essential to ensure the protection of sensitive data, prevent unauthorized access, and mitigate potential security risks. This guide outlines a step-by-step process for conducting a thorough security audit.

### 2. Scope of Audit

The security audit will encompass the following aspects:
- Access control and permissions for boards and members.
- Detection and prevention of sensitive data exposure.
- Integration and effectiveness of audit logs and monitoring.
- Integration of security practices and measures.

### 3. Account Access Control

#### Steps:
1. Review Board Access:
   - Assess the access control settings of each board.
   - Verify the members and collaborators for each board.
2. Principle of Least Privilege (PoLP):
   - Evaluate if board access is aligned with roles and responsibilities.
   - Identify and rectify overprivileged accounts.

#### Recommendations:
- Limit access to confidential boards to authorized individuals only.
- Regularly review and adjust board access based on member roles.

### 4. Sensitive Data Exposure

#### Steps:
1. Card Content Review:
   - Examine card titles and descriptions for sensitive information.
   - Ensure that sensitive data is not inadvertently exposed.
2. Attached Files Analysis:
   - Check for attached files or documents with improper access control.
   - Verify that confidential files are not accessible to unauthorized members.

#### Recommendations:
- Educate board members on not exposing sensitive data in card content.
- Implement proper access controls for attached files and documents.

### 5. Audit Logs and Monitoring

#### Steps:
1. Audit Log Review:
   - Examine audit logs for unusual or suspicious activities.
   - Monitor changes to board settings and permissions.
2. Member Activity Analysis:
   - Analyze the activity of board members.
   - Identify any anomalies in access or actions.

#### Recommendations:
- Regularly review audit logs to detect unauthorized activities.
- Set up notifications for unusual board access or activities.

### 6. Integrating Security Measures

#### Steps:
1. Security Bots or Plugins:
   - Explore security bots or plugins that monitor and prevent data sharing.
   - Integrate tools that can identify and alert for sensitive data exposure.
2. Member Training:
   - Provide training to board members on secure coding practices and data protection.
   - Educate members about the risks of exposing sensitive information.

#### Recommendations:
- Integrate security bots or plugins to monitor and prevent sensitive data sharing.
- Conduct regular security training sessions for board members.

### 7. Conclusion

Conducting a security audit of a Trello account is crucial to maintaining a secure environment for collaboration and data sharing. By following this comprehensive guide, you can identify vulnerabilities, mitigate risks, and implement best practices to enhance the overall security posture of your Trello account.

## Cloud Security Posture Assessment

### Google Cloud Platform (GCP)

1. **Identity and Access Management (IAM)**

- Review IAM roles, permissions, and policies to ensure the principle of least privilege.
- Implement multi-factor authentication (MFA) for user accounts.

2. **Network Security**

- Configure Virtual Private Cloud (VPC) with proper subnets and firewall rules.
- Utilize Cloud Identity-Aware Proxy (IAP) for secure access control.

3. **Data Security**

- Encrypt data at rest using Google Cloud KMS.
- Implement Data Loss Prevention (DLP) to prevent data leaks.

4. **Logging and Monitoring**

- Set up Google Cloud Logging and Monitoring for real-time insights.
- Create alerts for suspicious activities using Cloud Monitoring.

5. **Encryption**

- Use Customer-Supplied Encryption Keys (CSEK) for more control over encryption keys.
- Enable encryption in transit using HTTPS and SSL/TLS.

6. **Compliance and Auditing**

- Leverage Google Cloud Compliance programs for specific industry standards.
- Use Cloud Asset Inventory for compliance auditing.

### Microsoft Azure

1. **Identity and Access Management (IAM)**

- Review Azure Active Directory (Azure AD) roles and permissions.
- Implement Conditional Access policies for advanced access control.

2. **Network Security**

- Utilize Azure Virtual Network and Network Security Groups.
- Implement Azure Firewall for advanced network security.

3. **Data Security**

- Use Azure Disk Encryption and Azure Storage Service Encryption.
- Implement Azure Information Protection for data classification.

4. **Logging and Monitoring**

- Set up Azure Monitor and Log Analytics for comprehensive monitoring.
- Utilize Azure Security Center for threat detection and response.

5. **Encryption**

- Enable encryption at rest using Azure Key Vault.
- Implement Transport Layer Security (TLS) for data in transit.

6. **Compliance and Auditing**

- Utilize Azure Policy and Azure Blueprints for compliance enforcement.
- Leverage Azure Security Center's compliance assessment capabilities.

### Amazon Web Services (AWS)

1. **Identity and Access Management (IAM)**

- Review AWS Identity and Access Management (IAM) roles and policies.
- Implement AWS Multi-Factor Authentication (MFA) for user accounts.

2. **Network Security**

- Configure Amazon Virtual Private Cloud (VPC) with appropriate security groups and network ACLs.
- Utilize AWS Web Application Firewall (WAF) for protection against web-based attacks.

3. **Data Security**

- Implement AWS Key Management Service (KMS) for data encryption.
- Use AWS Macie for sensitive data discovery and protection.

4. **Logging and Monitoring**

- Set up Amazon CloudWatch for monitoring and alerts.
- Implement AWS CloudTrail for auditing and tracking.

5. **Encryption**

- Enable server-side encryption for Amazon S3 using AWS KMS.
- Utilize HTTPS and SSL/TLS for data in transit.

6. **Compliance and Auditing**

- Use AWS Config and AWS Trusted Advisor for compliance checks.
- Leverage AWS Security Hub for central security management.

## Conclusion

This sample report provides a comprehensive overview of cyber security best practices and measures to enhance the security posture of various aspects such as IAM policy management, GitHub security auditing, Trello security configuration, and cloud security posture assessment for different cloud platforms. By implementing these recommended practices, organizations can significantly reduce the risks associated with security misconfigurations, data exposure, and unauthorized access, ultimately ensuring a more secure environment for their projects and data.
