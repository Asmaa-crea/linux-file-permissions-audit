# Linux File Permissions Audit: Securing the Research Team Filesystem

## Project Description
As a Security Analyst for a large organization, my primary responsibility is to ensure system security and data integrity by maintaining proper access controls. In this project, I performed a security audit on the file system used by the research team (`/home/researcher2/projects`). The objective was to examine existing file and directory permissions, identify authorization anomalies that violate the organization's security policies (such as unauthorized write access), and use Linux commands to remediate these vulnerabilities.

## Scenario
The organization maintains a strict security policy stating that **"Other" users should never have write access to any files**, and sensitive departmental data must be restricted to authorized personnel only. My task was to investigate the `projects` directory, analyze the 10-character permission strings, modify permissions using `chmod` to eliminate unauthorized access, and restrict a sensitive subdirectory (`drafts`) exclusively to the primary researcher (`researcher2`).

## Check File and Directory Details
To investigate the current access controls, I navigated to the `/home/researcher2/projects` directory and listed all contents, including hidden files, using the following Linux command:

```bash
ls -la

Current File Permissions (Audit Results)
Based on the output of the command, the filesystem structure and permissions were as follows:

project_k.txt: -rwxrwxrwx (User: rw, Group: rw, Other: rw)

project_m.txt: -rw-r----- (User: rw, Group: r, Other: none)

project_r.txt: -rw-rw-r-- (User: rw, Group: rw, Other: r)

project_t.txt: -rw-rw-r-- (User: rw, Group: rw, Other: r)

.project_x.txt: -rw--w---- (User: rw, Group: w, Other: none) (Hidden File)

drafts/: drwx--x--- (User: rwx, Group: x, Other: none) (Subdirectory)

Describe the Permissions String
A Linux permission string consists of 10 characters (e.g., -rwxrwxrwx). Here is how to interpret this string:

1st Character: Represents the file type. A hyphen - indicates a regular file, while a d indicates a directory.

Characters 2–4 (User/Owner): Controls the read (r), write (w), and execute (x) permissions for the owner of the file.

Characters 5–7 (Group): Controls the read (r), write (w), and execute (x) permissions for the group assigned to the file.

Characters 8–10 (Other): Controls the read (r), write (w), and execute (x) permissions for any other users on the system.

Example Analysis from Audit:
For project_k.txt, the string is -rwxrwxrwx. This means it is a regular file where the User, Group, and Everyone else ("Other") all have full Read, Write, and Execute permissions. This severely violates our security policy.
