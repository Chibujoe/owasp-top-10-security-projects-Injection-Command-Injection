# A03: Command Injection Vulnerability (OWASP Top 10)

## Overview
This project demonstrates a Command Injection vulnerability in a web
application and shows how an attacker can exploit it to execute arbitrary
system commands. It also covers mitigation techniques to prevent the attack.

## Why This Matters
Command Injection vulnerabilities can lead to Remote Code Execution (RCE),
unauthorized access to sensitive files, service disruption, and full server
compromise if not properly handled.

## Lab Environment
- Web application built with PHP and HTML
- Local testing environment
- Attacker machine: Kali Linux

## Tools Used
- Kali Linux
- Web browser
- Linux shell utilities

## Vulnerability Description
The application accepts user input from a form and passes it directly into a
system command (`ping`) using `shell_exec()` without validation or sanitization.
This allows attackers to inject additional shell commands.

## Exploitation
The vulnerability was exploited by submitting the following payload:

