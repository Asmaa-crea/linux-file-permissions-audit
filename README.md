# Linux File Permissions Audit: Securing the Research Team Filesystem

## Project Description
As a Security Analyst for a large organization, my primary responsibility is to ensure system security and data integrity by maintaining proper access controls. In this project, I performed a security audit on the file system used by the research team (`/home/researcher2/projects`). The objective was to examine existing file and directory permissions, identify authorization anomalies that violate the organization's security policies (such as unauthorized write access), and use Linux commands to remediate these vulnerabilities.

## Scenario
The organization maintains a strict security policy stating that **"Other" users should never have write access to any files**, and sensitive departmental data must be restricted to authorized personnel only. My task was to investigate the `projects` directory, analyze the 10-character permission strings, modify permissions using `chmod` to eliminate unauthorized access, and restrict a sensitive subdirectory (`drafts`) exclusively to the primary researcher (`researcher2`).

## Check File and Directory Details
To investigate the current access controls, I navigated to the `/home/researcher2/projects` directory and listed all contents, including hidden files, using the following Linux command:

bash
ls -la


<img width="781" height="271" alt="image" src="https://github.com/user-attachments/assets/38a58c20-6bb4-4618-9bd5-883c6e35cae6" />



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

---

## Change File Permissions
During the audit, `project_k.txt` was flagged as a critical vulnerability because it allowed full write access to "Other" users (`-rwxrwxrwx`), which directly violates the organization's security policy. 

To fix this and ensure that "Other" users do not have write access, I executed the following command:

bash
chmod o-w project_k.txt
Explanation: The chmod command changes file permissions. The o-w flag explicitly removes (-) write access (w) from the "Other" (o) category, while leaving the User and Group permissions intact.

The following code demonstrates how I used Linux commands to do this:

<img width="794" height="281" alt="image" src="https://github.com/user-attachments/assets/d968143e-d013-40d6-82e1-3c592b1ac1ca" />

The first two lines of the screenshot display the commands I entered, and the other lines display the output of the second command. The chmod command changes the permissions on files and directories. The first argument indicates what permissions should be changed, and the second argument specifies the file or directory. In this example, I removed write permissions from other for the project_k.txt file. After this, I used ls -la to review the updates I made.

Change File Permissions on a Hidden File
The research team archived a hidden file named .project_x.txt. The organization's policy dictates that this archived file must not have write permissions for anyone, but both the User (owner) and the Group should retain read access.

To restrict write access and set the correct permissions, I ran:
chmod u-w,g-w,g+r .project_x.txt

Explanation: This command removes write permissions (-w) from both the User (u) and the Group (g), and explicitly ensures the Group has read access (g+r). This successfully locks down the archived file from accidental modifications while keeping it readable for authorized team members.

The following code demonstrates how I used Linux commands to change the permissions:

<img width="807" height="280" alt="image" src="https://github.com/user-attachments/assets/13a985ee-2343-48b8-b492-3f284b8bfad5" />


Change Directory Permissions
The drafts subdirectory contains sensitive, non-public research. According to the security briefs, only the primary researcher (researcher2) should have access to this directory and its contents. Group and Other users must have all access revoked.

To secure the directory, I used the following command:
chmod g-x,o= drafts

The following code demonstrates how I used Linux commands to change the permissions:

<img width="796" height="294" alt="image" src="https://github.com/user-attachments/assets/4965b09e-aafa-43e1-8811-334a75d036e9" />

Explanation: This command removes execute permissions from the Group (g-x) and completely strips all permissions from Other (o=), ensuring that only researcher2 (who holds rwx) can access, view, or execute scripts inside the drafts folder.

---

## Summary
Through this security audit, I successfully analyzed and remediated the file system permissions within the `/home/researcher2/projects` directory. By interpreting the 10-character Linux permission strings, I identified multiple compliance violations that compromised the integrity of the research team's data. 

Using targeted `chmod` commands, I eliminated unauthorized write access on standard files, secured archived hidden files, and completely isolated the sensitive `drafts` subdirectory to restrict access exclusively to `researcher2`. This practical exercise reinforces the importance of the Principle of Least Privilege and demonstrates a strong proficiency in utilizing Linux command-line tools to enforce organization-wide security policies.
