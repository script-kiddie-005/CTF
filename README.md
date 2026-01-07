# CTF
<!-- CTFs used as a practice environment to reinforce web security concepts and attack methodology. -->

This repository documents my approach to solving selected CTF challenges, focusing on web exploitation, logic analysis, and controlled bypass techniques


## CTF Overview
- Platform: picoCTF
- Category: Web Exploitation
- Skills Used: HTTP analysis, source code review, encoding techniques
- Tools: Burp Suite, browser dev tools


## Challenge 1: Break The Gate 1

### Objective
- This challenge involves investigating a restricted web portal where a user account is suspected of hiding sensitive data.
- While the login email is known, standard authentication attempts fail, hinting at a hidden access mechanism intentionally or unintentionally left by the developer.

### Approach
- Analyzed the login workflow by submitting invalid credentials to observe server-side responses and error handling.
- Inspected client-side resources and page source for unintended information disclosure.
- Identified obfuscated developer comments that hinted at a non-standard authentication bypass.
- Decoded the obfuscated content to uncover a required custom HTTP header.
- Intercepted and modified the authentication request to include the identified header.
- Validated the bypass by replaying the request and confirming unauthorized access through the server response.

### Key Finding
- The application exposed a hidden authentication bypass through obfuscated developer comments in the client-side source code.
- When decoded, these comments revealed a custom HTTP header that the server trusted for access control, allowing authentication to be bypassed without valid credentials.

### Outcome
- Successfully bypassed the authentication mechanism and gained unauthorized access to the restricted portal, confirming the presence of a critical access control flaw.
