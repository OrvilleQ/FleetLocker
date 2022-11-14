# FleetLocker

**FleetLocker** is a reboot coordinator for Fedora CoreOS nodes powered by Cloudflare Workers®. It implements the [FleetLock](https://coreos.github.io/zincati/development/fleetlock/protocol/) protocol for use as a [Zincati](https://github.com/coreos/zincati) lock [strategy](https://github.com/coreos/zincati/blob/master/docs/usage/updates-strategy.md) backend.

## Usage

Zincati runs on-host (`zincati.service`). Declare a Zincati `fleet_lock` strategy when provisioning Fedora CoreOS nodes. Set `base_url` for host nodes to access the `FLeetLocker` Service.

```yaml
variant: fcos
version: 1.4.0
storage:
  files:
    - path: /etc/zincati/config.d/55-update-strategy.toml
      contents:
        inline: |
          [updates]
          strategy = "fleet_lock"
          [updates.fleet_lock]
          base_url = "https://fleetlocker.example.workers.dev"
```

### Configuration

Configuration the server via environment variables.

| variable       | description | default       |
|----------------|-------------|---------------|
| `KVNAMESPACE`  | KVNamespace | "FLEETLOCKER" |

## Manual Intervention

## Related

* [Zincati Guide](https://docs.fedoraproject.org/en-US/fedora-coreos/auto-updates/)
* [Zincati Docs](https://github.com/coreos/zincati/blob/master/docs/usage/updates-strategy.md)
* [FleetLock Protocol](https://coreos.github.io/zincati/development/fleetlock/protocol/)
* [`fleetlock`](https://github.com/poseidon/fleetlock) by [poseidon](https://github.com/poseidon)