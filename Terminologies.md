Lecture 17.

- NGINX master process (runs as root)
- NGINX worker process (runs as www-data)
- Digital Ocean
    - Droplet
- NGINX installation
  - via operating-system package managers (`apt-get` / `yum`).
  - via install & build from source code.

- `nginx.conf`
- Context
    - `Main / Global` 
    - `events`
    - `http`
    - `server`
    - `location`
    - `upstream`
    - `mail`
- Directive
    - `include`
    - `listen`
    - `proxy_pass`
    - `fastcgi_pass`
    - `location`
    - `proxy_set_header`
    - `log_format`
    - `add_header`
    - `gzip Directives`
      - `gzip`
      - `gzip_min_length`
      - `gzip_comp_level`
      - `gzip_types`
    - `fastcgi Cache Directives`
      - `fastcgi_cache_path`
      - `fastcgi_cache_key`
      - `fastcgi_cache`
      - `fastcgi_cache_valid`
    - `Proxy Cache Directives`
      - `proxy_cache_path`
      - `proxy_cache_key`
      - `proxy_cache`
      - `proxy_cache_valid`
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
        - `$scheme`
        - `$request_method`
        - `$host`
        - `$request_uri`
        - `$upstream_cache_status`
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
- Gzip compression
- Transferred Data vs. Resource Size
- Note: Compression Uses Server Resources (CPU)
- Gzip Compression Level
  - `1` → Lowest compression, fastest 
  - `2–3` → Low compression 
  - `4–6` → Moderate/practical compression 
  - `7–8` → High compression 
  - `9` → Maximum compression, slowest
- Note: Do not configure Gzip for `.jpg`, `.jpeg`, and `.png` images because these formats are already compressed.
- Note: When testing manually with `curl` client must explicitly indicate its support for compressed content, A request without an appropriate `Accept-Encoding` header does not necessarily cause NGINX to return the compressed representation.
- Note: `gzip_min_length` default value is `20 bytes`
- Hard refresh vs Soft refresh (Browser)
- Cache Busting: a technique web developers use to force a browser to load the newest version of a static file (such as CSS or JavaScript) instead of a previously saved, stale copy

- Caching Types
  - Client-Side Caching (Static Content)
  - Server-Side Caching (Dynamic Content)
    - Types
      - Normal Caching: caching a dynamic response for X amount of time
      - Micro Caching: caching a dynamic response for a very short period, usually a few seconds
        - Public Content: No need for cache key (most useful for)
        - Personalized Content: unique cache key needed for each user (like `proxy_cache_key "$scheme$request_method$host$request_uri$cookie_session_id";`)
    - Types
      - Proxy Cache
      - FastCGI Cache

### HTTP Headers
- `X-Real-IP`
- `X-Forwarded-For`
- `Content-Encoding: gzip`
- `Cache-Control`
  - `Cache-Control: public`: response can be cached not only by the end user's browser, but also by intermediate
    proxy/cache servers
  - `Cache-Control: private`: indicates that the response should only be cached by the end client.
  - `Cache-Control: public|private, max-age=<seconds>`: specifies how long a resource can remain cached before it is
    considered stale.
- `Expires: <specific-date>`
- Note: When `max-age` and `Expires` are present, `max-age` takes precedence.
- `Pragma`: deprecated counterpart to `Cache-Control`.
- `Vary` : It tells caches which request headers can affect the representation of the response.
  - `Vary: Accept-Encoding`: Like saying cache this response, pay attention to Accept-Encoding because the response can
    change depending on whether the client supports gzip, etc.
  - `Vary: Accept-Language`: The response changes based on the client's preferred language.
  - `Vary: *`: it prevents a cache from using the response for subsequent requests.

### NginX Modules used

- `--with-http_image_filter_module=dynamic`
- `--with-http_realip_module`

### HTTP Status Codes
- `304` → Not Modified

### Linux Commands
- `curl -Ik` (...)
- Apache Bench (`ab`)