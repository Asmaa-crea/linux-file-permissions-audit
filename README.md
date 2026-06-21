# Linux File Permissions Audit: Securing the Research Team Filesystem

## Project Description
As a Security Analyst for a large organization, my primary responsibility is to ensure system security and data integrity by maintaining proper access controls. In this project, I performed a security audit on the file system used by the research team (`/home/researcher2/projects`). The objective was to examine existing file and directory permissions, identify authorization anomalies that violate the organization's security policies (such as unauthorized write access), and use Linux commands to remediate these vulnerabilities.

## Scenario
The organization maintains a strict security policy stating that **"Other" users should never have write access to any files**, and sensitive departmental data must be restricted to authorized personnel only. My task was to investigate the `projects` directory, analyze the 10-character permission strings, modify permissions using `chmod` to eliminate unauthorized access, and restrict a sensitive subdirectory (`drafts`) exclusively to the primary researcher (`researcher2`).
