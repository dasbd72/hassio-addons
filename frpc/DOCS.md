# Home Assistant Add-on: FRP Client

## Installation

1. Add this repository to your Home Assistant instance's add-on store.
2. Install the "FRP Client" add-on.
3. Configure it as described below.
4. Start the add-on.

## Configuration

Example add-on configuration:

```yaml
server_addr: frp.example.com
server_port: 7000
token: super-secret-token
proxies:
  - name: homeassistant
    type: http
    local_ip: 127.0.0.1
    local_port: 8123
    custom_domains:
      - ha.example.com
  - name: ssh
    type: tcp
    local_ip: 127.0.0.1
    local_port: 22
    remote_port: 2222
    custom_domains: []
```

### Option: `server_addr`

Hostname or IP address of your frp server.

### Option: `server_port`

Port your frp server listens on (typically `7000`).

### Option: `token`

Authentication token configured on your frp server (`auth.token` in
`frps.toml`).

### Option: `proxies`

A list of proxies to expose. Each entry supports:

- `name`: A unique name for the proxy.
- `type`: One of `http`, `tcp`, or `udp`.
- `local_ip`: IP address of the local service (usually `127.0.0.1` or the
  Home Assistant hostname).
- `local_port`: Port of the local service.
- `custom_domains`: List of domains to route to this proxy. Only used when
  `type` is `http` (or `https`); set to `[]` for `tcp`/`udp` proxies.
- `remote_port`: Port to expose on the frp server. Only used when `type` is
  `tcp` or `udp`. If omitted, the server assigns a port automatically
  (requires `allow_ports`/random port assignment to be enabled in
  `frps.toml`).

## Notes

- Only token-based authentication is currently supported.
- The generated frpc configuration is written to `/tmp/frpc.toml` on every
  start and is not meant to be edited by hand.
