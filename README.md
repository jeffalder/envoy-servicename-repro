## Repro case

repro for: https://github.com/envoyproxy/envoy/issues/23475

### How to run

```sh
docker compose up &
curl localhost:7572
```

Watch for the `mitmproxy` container logs.

### What problem are we reproducing?

The problem is that the span (in the `mitmproxy` container logs) has this:

```json
            "localEndpoint": {
                "ipv4": "172.18.0.3",
                "port": 0
            },
```

This span won't be accepted by New Relic because it doesn't set `localEndpoint.serviceName` and I can't figure out how to get that set.
