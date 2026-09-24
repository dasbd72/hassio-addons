# Changelog

## 0.1.4

- Adds an optional `remote_port` proxy option for specifying the remote
  port to use on the frp server for `tcp`/`udp` proxies.
- Makes `custom_domains` optional, since it only applies to `http` proxies.

## 0.1.3

- Sets `init: false` in `config.yaml`. Without it, Supervisor injects its
  own init (tini) as PID 1, which conflicts with the base image's
  s6-overlay init and causes `s6-overlay-suexec: fatal: can only run as
  pid 1`.

## 0.1.2

- Fixes `bashio::config` returning `null` for all options, which crashed
  frpc. The build step was deleting `curl`, which `bashio` requires at
  runtime to call the Supervisor API.

## 0.1.1

- Fixes a bug where the add-on would not start.

## 0.1.0

- Initial release.
- Generates frpc configuration from add-on options and runs the frp client.
- Supports `http`, `tcp`, and `udp` proxies with token authentication.
