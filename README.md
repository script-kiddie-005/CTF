# CTF
<!-- CTFs used as a practice environment to reinforce web security concepts and attack methodology. -->

This repository documents my approach to solving selected CTF challenges, focusing on web exploitation, logic analysis, and controlled bypass techniques


## CTF Overview
- Platform: picoCTF
- Category: Web Exploitation
- Skills Used: HTTP analysis, source code review, encoding techniques
- Tools: Burp Suite, browser dev tools


### Challenge 1: Break The Gate 1

#### Objective
- This challenge involves investigating a restricted web portal where a user account is suspected of hiding sensitive data.
- While the login email is known, standard authentication attempts fail, hinting at a hidden access mechanism intentionally or unintentionally left by the developer.

#### Approach
- Analyzed the login workflow by submitting invalid credentials to observe server-side responses and error handling.
- Inspected client-side resources and page source for unintended information disclosure.
- Identified obfuscated developer comments that hinted at a non-standard authentication bypass.
- Decoded the obfuscated content to uncover a required custom HTTP header.
- Intercepted and modified the authentication request to include the identified header.
- Validated the bypass by replaying the request and confirming unauthorized access through the server response.

#### Key Finding
- The application exposed a hidden authentication bypass through obfuscated developer comments in the client-side source code.
- When decoded, these comments revealed a custom HTTP header that the server trusted for access control, allowing authentication to be bypassed without valid credentials.

#### Outcome
- Successfully bypassed the authentication mechanism and gained unauthorized access to the restricted portal, confirming the presence of a critical access control flaw.


### Challenge 2: SSTI 1

#### Objective
- To exploit a Server-Side Template Injection (SSTI) vulnerability in a web application challenge from picoCTF, identify the underlying templating engine, and retrieve the challenge flag by executing code on the server.

#### Approach
- Started by observing how the web app rendered user input after submission.
- Recognized from the challenge title (SSTI1) that it likely involved server-side template injection.
- Tested template expressions such as {{7*'7'}}, which executed and returned results, confirming SSTI.
- Enumerated internal objects to identify that the server used Jinja2 as the template engine.
- Leveraged access to Python globals and built-ins exposed through Jinja2 to import the os module and run shell commands to explore the file system.

#### Key Finding
- The target was vulnerable to Server-Side Template Injection because user input was directly interpreted by a server template engine without proper sanitization.
- Successful template expressions like {{7*'7'}} confirmed that input was executed as code.
- By examining internal objects, it was determined that Jinja2 was the engine used, opening paths to further exploitation.
- Using Python’s os module through Jinja2 globals allowed execution of commands like ls and cat flag, ultimately retrieving the challenge flag.

#### Outcome
- The vulnerability was successfully exploited by injecting template expressions that triggered code execution via the Jinja2 engine.
- This allowed retrieval of the challenge flag and demonstrated a fundamental SSTI attack flow in a controlled CTF environment.
