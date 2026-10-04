Lecture 17.

- NGINX master process (runs as root)
- NGINX master process (runs as www-data)
- Digital Ocean
  - Droplet

- install NGINX via operating-system package managers.
- install & build NGINX from source code.


- `nginx.conf`
- Context
  - events Context
  - http Context
  - server Context
  - location Context
  - upstream Context
  - mail Context
- Main / Global Context
- Directive
- NGINX uses an event-based connection processing model
- Active and Passive/Fallback Servers (?)
- SCP (Secure Copy Protocol)
- location context modifier
  - no modifier → prefix match
  - `=` → exact match modifier
  - `~` → case-sensitive regular expression
  - `~*` → case-insensitive regular expression
  - `^~` → Preferential prefix match
- Location Matching Priority `= > ^~ > ~* > ~ | (no modifier)`
- Variables
  - User-Defined Variables (`set $variable value;`)
  - Built-In NGINX Variables
    - `$args`
    - `$body_bytes_sent`
    - `$body_bytes_received`
    - `$connection_requests`
    - `$date_local`
    - `$hostname`
    - `$nginx_version`
- `$arg_<name>` Pattern
- `return` Directive (`return <status-code> <URL-or-response>;`)
  - Its resource consumption is lower than `rewrite`
- `rewrite` Directive (`rewrite <regex> <replacement> [flag];`)
  - Capturing Values with Rewrite 