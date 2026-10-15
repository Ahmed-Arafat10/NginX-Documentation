- NGINX master process (runs as root)
- NGINX worker process (runs as www-data)
- Digital Ocean
    - Droplet
- NGINX installation
  - via operating-system package managers (`apt-get` / `yum`).
  - via install & build from source code.

- HTTP Properties
  - Connectionless
  - Media Independent
  - Stateless

- HTTP Request Structure
  - Request line
    - Method Token
    - Request URI
    - Protocol version
  - Zero or more headers
  - An empty line
  - Message body (optional)

- `nginx.conf`
- Context
    - `Main / Global` 
    - `events`
    - `http`
    - `server`
    - `location`
    - `upstream`
      - `least_time header|last_byte;`
        - `least_conn;`
      - `ip_hash;`
      - `weight;` (Parameter)
    - `mail`
- Directive
    - `Core`
      - `user`
      - `worker_processes`
      - `worker_connections`
      - `pid`
      - `load_module`
      - `access_log`
      - `error_log`
    - `include`
    - `listen`
    - `server_name`
    - `root`
    - `index`
    - `types`
    - `return`
    - `rewrite`
    - `try_files`
    - `set`
    - `if`
    - `client_body_buffer_size`
    - `client_header_buffer_size`
    - `client_max_body_size`
    - `large_client_header_buffers`
    - `client_body_timeout`
    - `client_header_timeout`
    - `keepalive_timeout`
    - `send_timeout`
    - `expires`
    - `fastcgi_cache_bypass` [NEW]
    - `fastcgi_no_cache` [NEW]
    - `proxy_http_version` [NEW]
    - `proxy_next_upstream` [NEW]
    - `proxy_next_upstream_tries` [NEW]
    - `resolver` [NEW]
    - `image_filter`
    - `ssl_certificate`
    - `ssl_certificate_key`
    - `http2`
    - `sendfile`
    - `tcp_nopush`
    - `tcp_nodelay`
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
    - `Rate Limiting`
      - `limit_req_zone`
      - `limit_req`
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
        - `$server_name`
        - `$server_port`
        - `$binary_remote_addr`
        - `$remote_addr`
        - `$uri`
        - `$document_root` [NEW]
        - `$document_uri`
        - `$proxy_add_x_forwarded_for`: Automatically appends `$remote_addr` to incoming `X-Forwarded-For` header.
        - `$remote_user`
        - `$time_local`
        - `$request`
        - `$status`
        - `$http_referer`
        - `$http_user_agent`
        - `$http_<header_name>`** — Built-in prefix allowing reading of arbitrary client HTTP request headers (e.g., `$http_x_real_ip`).
        - `$server_protocol`
        - `$arg_<name>` Pattern
        - `$1`, `$2`: Positional regex capture groups created by `rewrite` or regular expression `location` directives.
        - `$request_id`
        - `$request_time`
        - `$upstream_response_time`

- `return` Directive (`return <status-code> <URL-or-response>;`) [?-More Examples]
    - Its resource consumption is lower than `rewrite`
- `rewrite` Directive (`rewrite <regex> <replacement> [flag];`) [???]
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

- Leaky Bucket Algorithm (rate limiting used by NginX)

- Server Pool: A group of servers capable of handling application requests.
- Failover:	Redirecting traffic away from an unavailable server.
- Auto-scaling: Increasing the number of application servers when demand increases.
- Auto-descaling: Reducing the number of application servers when demand decreases.

- Expensive Requests
- DNS Round Robin
- DNS A records (Address Record)
````
app.example.com. 300 IN A 192.0.2.10
````
This is a standard DNS A record configuration entry, typically found in a DNS zone file.
Here is a breakdown of what each component means:
- app.example.com.: The Domain Name (or hostname) being configured. The trailing dot indicates it is a Fully Qualified Domain Name (FQDN).
- 300: The TTL (Time to Live) in seconds. This tells DNS resolvers and browsers to cache this specific record for 5 minutes before checking for updates again.
- IN: The Class of the record, which stands for Internet. This is the standard class used for almost all modern DNS records.
- A: The Record Type. An A record (Address record) maps a hostname directly to an IPv4 address.
- 192.0.2.10: The Value (or target), which is the specific IPv4 address where traffic for app.example.com will be routed.


- Load Balancer Functions
  - Distribute traffic efficiently
  - Support failover (Ensure high availability and reliability)
  - Support auto-scaling and auto-descaling

- Load-Balancing Algorithms
  - Round Robin
  - Least Connections (TODO: add how it is done in lec 43)
  - Least Response Time (Nginx Plus Needed) (TODO: add how it is done in lec 43)
  - Least Bandwidth (No directive for it)
  - Hashing (TODO: add how it is done in lec 43)

- Related Load-Balancing Fundamentals
  - Session persistence (sticky routing): Directing requests belonging to the same session to the same server.
    - `ip_hash` is not identical to full session persistence in every situation. Users behind the same NAT gateway may share an IP address, and a server failure or upstream membership change can affect routing.
    - Where possible, applications should use shared session storage or stateless authentication so that any healthy backend can handle a request. This reduces dependence on sticky routing.
  - Dynamic Configuration of Server Groups (auto-scaling / auto-descaling)
    - Note: Dynamic scaling requires integration with infrastructure provisioning, monitoring, orchestration, or cloud-management mechanisms. The load balancer alone does not necessarily perform the entire scaling process.

- Hardware vs. Software Load Balancing

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
  - `Cache-Control: No-Cache`: Requires the cache to revalidate the stored response with the origin server before using it. [???]
  - `Cache-Control: No-Store`: Prevents caches from storing the request or response. (used with sensitive data)
- `Expires: <specific-date>`
- Note: When `max-age` and `Expires` are present, `max-age` takes precedence.
- `Pragma`: deprecated counterpart to `Cache-Control`.
- `Vary` : It tells caches which request headers can affect the representation of the response.
  - `Vary: Accept-Encoding`: Like saying cache this response, pay attention to Accept-Encoding because the response can
    change depending on whether the client supports gzip, etc.
  - `Vary: Accept-Language`: The response changes based on the client's preferred language.
  - `Vary: *`: it prevents a cache from using the response for subsequent requests.
- `Last-Modified`: Date/time file was last modified on disk.
- `ETag`: Entity tag validator for conditional client caching. [NEW]
- `Transfer-Encoding`: Form of encoding applied to payload (e.g., `chunked`) [???]
- `Content-Length`: Body size in bytes.

### NginX Modules used

- `--with-http_image_filter_module=dynamic`
- `--with-http_realip_module`
- `--with-http_v2_module`

### HTTP Status Codes
- `304` → Not Modified
- `429` → Too Many Requests *(Rate limit rejection)*
- `301` → Moved Permanently
- `307` → Temporary Redirect *(Preserves HTTP request method)*

### Linux Commands
- `curl -Ik`
- Apache Bench (`ab`)
- Siege (HTTP Load Tester)