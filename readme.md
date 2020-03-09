
# Remmie

A remote-code and API execution tool designed to work around
NAT routers, firewalls, and other poorly-deployed network architecture
to connect two machines in a standardized manner. Remmie plays nicely
with existing infrastructure such as SSH servers, PSEXEC, and HTTP/S API endpoints.

## Usage 

```bash
# SSH and psexec commands are shell commands and their stdout,sterr, and stdin are
# forwarded to the terminal running `remmie`
remmie ssh://user@host 'uname -a'
remmie ssh://alias 'uname -a'

remmie psexec://user@host 'ipconfig /all'

# HTTP "commands" are not shell commands but a DSL consisting of:
# <METHOD>:<URL Keys and Values>
# Value entries prefixed with '@' will be parsed as file paths and uploaded
# Example: POST:username=Janet Smith&profileImg=@/tmp/janet.jpg
# If your value requires a literal '@' simply URLEncode it:
# Example: POST:username=Janet Smith&twitterName=%40janet_smith_123

# Default HTTP stdout is the body from the server.
# If you need to configure details of output remmie parses
# several URI parameters:

remmie http://host:8080 'GET:key1=val_1&key2=Value Two'
remmie http://host:8080 'POST:key1=val_1&key2=Value Two'

# The 'output' URI parameter takes 3 arguments specifying what
# response data is printed to stdout: [raw, body, headers].
remmie http://host:8080?output=raw 'POST:key1=val_1&key2=Value Two'
remmie http://host:8080?output=body 'POST:key1=val_1&key2=Value Two'
remmie http://host:8080?output=headers 'POST:key1=val_1&key2=Value Two'
# When using 'output=headers' the parameter 'header-names' can specify a
# comma-seperated list of specific headers to output.
# If a single value is specified for 'header-names' the header will not be printed
remmie http://host:8080?output=headers&header-names=Server 'POST:key1=val_1&key2=Value Two'
# ^ Example output: "Apache"
remmie http://host:8080?output=headers&header-names=Server,Date 'POST:key1=val_1&key2=Value Two'
# ^ Example output (2 lines): "Server: Apache\r\nDate: Mon, 09 Mar 2020 18:25:58 GMT"

```

## Status

 - [X] Hello World compiles
 - [ ] Argument and URI parsing
 - [ ] Config file parsing

---

 - [ ] SSH backend
 - [ ] psexec backend
 - [ ] WMI backend
 - [ ] http/s backend
 - [ ] telnet backend
 - [ ] tcp/udp backends (one-way data push + receive, nothing fancy)

---

 - [ ] Plan User Script system (config, environment, and permission handling mostly)
 - [ ] User Scripts executed to process stdout
 - [ ] User Scripts to push stdin/automate multiple API calls

---

 - [ ] Plan some protocol-discovery (user gives credentials + we try SSH/psexec/WMI/etc)
 - [ ] Plan some host-discovery (user has a smart lightbulb they'd like to talk to but has no idea where it is on the LAN)

