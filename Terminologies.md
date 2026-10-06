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
  - `events`
  - `html`
  - `server`
  - `include`
  - `listen`
  - `proxy_pass`
  - `fastcgi_pass`
  - `location`
  - `proxy_set_header`
  - `log_format`
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
- `try_files`
- catch-all block (`location /`)
- FastCGI
- Forward Proxy
- Reverse Proxy
  - Load balancing
  - Protection against attacks
    - DOS
    - Rate Limiting
  - Caching
  - SSL/TLS encryption handling
- NetTools (Linux)
- Client-Side Caching


### NginX Modules used
- `--with-http_image_filter_module=dynamic`
- `--with-http_realip_module`