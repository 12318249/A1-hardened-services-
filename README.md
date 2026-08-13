COIT12202: Network Security Concepts (HT2,2026)

Password Security A1 hardened security 



Student Name: Hiralben Hemantkumar Thakkar 

Unit: hardend services portfolio 

Date: 10/08/26



1. Introduction
   
Password security plays a vital role in protecting systems and maintaining cybersecurity within organisations. In this assessment, I configured password policies on a Linux system using Pluggable Authentication Modules (PAM). The aim was to demonstrate how strong password rules can be applied, how password history can be enforced, and how secure hashing methods can be verified. All findings were supported with practical testing and screenshots.


2. PAM Configuration and System Hardening

2.1 Overview of PAM
Pluggable Authentication Modules (PAM) allow Linux systems to manage authentication through a flexible, modular setup. The file located at /etc/pam.d/common-password controls password requirements for all system services. By adjusting this file, administrators can apply password standards that meet organisational security needs.


2.2 Setting Up Password Complexity Rules


To strengthen password security, I added the following rule:
Code
password requisite pam_pwquality.so retry=3 minlen=12 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1
This configuration requires:
•	A minimum of 12 characters
•	At least one uppercase letter
•	At least one lowercase letter
•	At least one number
•	At least one special character
•	Up to three attempts before failure
These settings follow current cybersecurity recommendations for creating strong and secure passwords.



2.3 Password History Enforcement

To stop users from reusing old passwords, I applied this rule:
Code
password [success=1 default=ignore] pam_unix.so obscure use_authtok try_first_pass yescrypt remember=5
This prevents users from reusing any of their last five passwords. Enforcing password history helps reduce repeated weak passwords and supports organisational compliance.


2.4 Secure Hashing (yescrypt)

The system uses yescrypt, a modern hashing algorithm designed to resist brute force attacks. Hashing protects passwords by storing them in a secure, irreversible format. The presence of $y$ in the /etc/shadow file confirms that yescrypt hashing is enabled and functioning correctly.


3. Evidence of System Behaviour
   
3.1 Weak Password Rejection

I tested a weak password (“abc”) using the passwd command. The system rejected it because it did not meet the complexity requirements.

<img width="519" height="235" alt="image" src="https://github.com/user-attachments/assets/97a8aff8-435f-44d9-b1b9-1daff2ccfc31" />

 
3.2 Password History Enforcement

After setting a strong password, I attempted to reuse the same one. The system refused the change due to the remember=5 rule.


<img width="594" height="335" alt="Screenshot 2026-08-13 at 3 57 49 PM" src="https://github.com/user-attachments/assets/23fefe1e-aa06-4e3c-8647-4646433ffed9" />

  

3.3 Shadow File Hashing Evidence

To confirm secure hashing, I viewed the /etc/shadow file using:
Code
cat /etc/shadow
The password hash began with $y$, showing that yescrypt hashing is active.


<img width="596" height="339" alt="Screenshot 2026-08-13 at 3 58 05 PM" src="https://github.com/user-attachments/assets/fc1bb554-3460-4dca-b88a-fa02ae1db58b" />

  

4. Password Rotation Policy

Regular password changes are still used in many organisations, even though modern guidelines recommend avoiding overly frequent rotation. In this assessment, password rotation was demonstrated through the remember=5 rule, which prevents users from reusing their five most recent passwords. This ensures that every password change results in a new and unique credential.
Importance of Password Rotation
•	Limits long-term exposure of compromised passwords
•	Prevents repeated use of predictable or weak passwords
•	Helps organisations meet compliance requirements
•	Strengthens overall authentication security



5. Conclusion

This assessment showed how password security controls can be effectively implemented in a Linux environment. By configuring PAM modules, enforcing strong password complexity, preventing password reuse, and verifying secure hashing, the system now meets recommended security standards. The practical testing and screenshots clearly demonstrate that the configuration works as intended. Completing this task improved my understanding of authentication policies and highlighted the importance of maintaining secure password practices within organisations.




APA 7th Edition References

Australian Cyber Security Centre. (2023). Essential Eight maturity model. https://www.cyber.gov.au
Debian Project. (2024). PAM and authentication documentation. https://www.debian.org/doc/
Linux Manual Pages. (2024). pam_pwquality(8) and pam_unix(8). https://man7.org/linux/man-pages/
National Institute of Standards and Technology. (2017). Digital identity guidelines: Authentication and lifecycle management (SP 800 63B). https://doi.org/10.6028/NIST.SP.800-63b

