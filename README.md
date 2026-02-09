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

The semicolon (`;`) acts as a command separator, allowing the injected `ls -la`
command to execute after the intended `ping` command. This resulted in the
server displaying a directory listing, confirming command execution.

## Impact
- Arbitrary command execution
- Exposure of sensitive system files
- Potential system compromise
- Denial of Service (DoS)

## Mitigation
The vulnerability was fixed by sanitising user input using PHP’s
`escapeshellcmd()` function before executing the system command.

Additional security measures include:
- Strict input validation (allowlisting domains/IPs)
- Using `escapeshellarg()` for arguments
- Avoiding system commands where possible
- Running services with least privilege

## Outcome & Lessons Learned
This project reinforced the importance of input validation and secure handling
of user-supplied data. Even simple applications can become dangerous if user
input is trusted blindly.

## Disclaimer
This project is for educational purposes only.

## Vulnerability Description
The application accepts user input from a form and passes it directly into a
system command (`ping`) using `shell_exec()` without validation or sanitization.
This allows attackers to inject additional shell commands.

## Exploitation
The vulnerability was exploited by submitting the following payload:
## Vulnerable-app/command.php
<?php
if (isset($_POST['domain'])) {
    $domain = $_POST['domain'];

    // Vulnerable to command injection
    $output = shell_exec("ping -c 4 " . $domain);
    echo "<pre>$output</pre>";
}
?>
## fixed-app/command.php
<?php
if (isset($_POST['domain'])) {
    $domain = $_POST['domain'];

    // Mitigated version
    $safe_domain = escapeshellcmd($domain);
    $output = shell_exec("ping -c 4 " . $safe_domain);
    echo "<pre>$output</pre>";
}
?>

## Screenshots
<img width="736" height="427" alt="image" src="https://github.com/user-attachments/assets/c8ae0fb4-5427-4258-ad7e-d95ae1e62ace" />



