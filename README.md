# k8s-cert-expiry

> Know which certificate expires first, before the pager tells you.

**Status:** 🚧 In development

## Overview

Report expiring TLS secrets and cert-manager Certificates across a cluster, sorted by days remaining, with an exit code suitable for a CI gate.

## Features

- Scans every `kubernetes.io/tls` secret in the cluster and parses the leaf certificate out of `tls.crt`
- Includes cert-manager `Certificate` resources with their Ready condition and next renewal time
- Sorted by days remaining, showing subject, SANs, issuer and the secret that holds it
- `--warn` and `--critical` thresholds drive the exit code, so it works unchanged as a CI or cron gate
- Namespace, label and issuer excludes for internal CA bundles and service-mesh certs that rotate themselves
- JSON output for feeding an alerting pipeline instead of a human

## Stack

Go + client-go, crypto/x509 for parsing, the cert-manager client-go for Certificate resources, and cobra.

## Usage

```bash
k8s-cert-expiry --all-namespaces --warn 30d --critical 7d --output table
```

## License

MIT

---

Archived on 2026-11-05. The idea moved to [certcheck](https://github.com/moveeeax/certcheck/issues/15).
