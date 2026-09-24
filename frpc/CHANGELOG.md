# Changelog

## 0.1.0

- Initial release.
- Generates frpc configuration from add-on options and runs the frp client.
- Supports `http`, `tcp`, and `udp` proxies with token authentication.

## 0.1.1

- Fixes a bug where the add-on would not start.

## 0.1.2

- Fixes `bashio::config` returning `null` for all options, which crashed
  frpc. The build step was deleting `curl`, which `bashio` requires at
  runtime to call the Supervisor API.
