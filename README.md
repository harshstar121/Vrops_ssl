# vROps / Aria Operations SSL Post-Renewal Validation Framework

Ansible-based regression framework for validating a vROps/Aria Operations
certificate renewal performed through vRealize Suite Lifecycle Manager (vRSLCM).

## What it validates

- TLS certificate reachability
- Certificate expiry threshold
- Subject Alternative Names
- Issuer
- vROps Product UI
- vROps Admin UI
- vROps REST API
- Adapter inventory endpoint
- Cloud Proxy/Remote Collector endpoint
- vRSLCM health
- vRSLCM environment inventory
- Authenticated API smoke test

## Important

API paths and response schemas differ across Aria Operations/vRSLCM releases.
The framework deliberately keeps release-specific endpoints configurable rather
than pretending one URI works for every version.

Before production use:
1. Set the correct API paths for your release.
2. Replace example FQDNs.
3. Encrypt credentials with Ansible Vault.
4. Add release-specific JSON assertions for cluster, adapter, collection and
   inventory-sync state.

## Run

ansible-playbook -i inventories/prod/hosts.yml site.yml \
  --ask-vault-pass

Reports are written to:

output/<RUN_ID>/report.html
output/<RUN_ID>/report.csv
output/<RUN_ID>/results.json

## Recommended next extensions

- Exact cluster/node health API assertions
- Exact adapter collection-state assertions
- Exact vRSLCM Inventory Sync operation polling
- SSO/LDAP login test
- Metric freshness test
- Alert/notification test
- Post-renewal log scan
- JUnit XML for CI/CD
- Email/Teams/ServiceNow notification
