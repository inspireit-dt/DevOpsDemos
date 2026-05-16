# GCP Custom Role Creation Commands

**Organization ID:** `692154983500` (simplelinks.co)

---

## Role 1: SimpleLinks Security Viewer

Read-only access to IAM policies, audit logs, org policies, and Cloud Asset Inventory.

```bash
gcloud iam roles create simplelinks_security_viewer \
  --organization=692154983500 \
  --title="SimpleLinks Security Viewer" \
  --description="Read-only access to IAM policies, audit logs, org policies, and Cloud Asset Inventory" \
  --stage=GA \
  --permissions="iam.roles.get,iam.roles.list,iam.serviceAccounts.getIamPolicy,resourcemanager.projects.getIamPolicy,resourcemanager.folders.getIamPolicy,logging.logEntries.list,logging.logs.list,orgpolicy.policies.list,orgpolicy.policy.get,cloudasset.assets.listResource,cloudasset.assets.queryAccessPolicy"
```

### Verify

```bash
gcloud iam roles describe simplelinks_security_viewer --organization=692154983500
```

---

## Role 2: SimpleLinks Network Admin

Full CRUD on compute networking, DNS, interconnects, and forwarding rules.

```bash
gcloud iam roles create simplelinks_network_admin \
  --organization=692154983500 \
  --title="SimpleLinks Network Admin" \
  --description="Full CRUD on compute networking, DNS, interconnects, and forwarding rules" \
  --stage=GA \
  --permissions="compute.networks.create,compute.networks.update,compute.networks.delete,compute.subnetworks.create,compute.subnetworks.update,compute.subnetworks.delete,compute.subnetworks.get,compute.subnetworks.list,compute.subnetworks.setPrivateIpGoogleAccess,compute.firewalls.create,compute.firewalls.update,compute.firewalls.delete,compute.routes.create,compute.routes.delete,compute.routes.get,compute.routes.list,dns.managedZones.create,dns.managedZones.update,dns.managedZones.delete,dns.managedZones.get,dns.managedZones.list,compute.interconnects.create,compute.interconnects.update,compute.interconnects.delete,compute.interconnects.get,compute.interconnects.list,compute.forwardingRules.create,compute.forwardingRules.update,compute.forwardingRules.delete,compute.forwardingRules.get,compute.forwardingRules.list"
```

> **Note:** `compute.networks.update` and interconnect permissions are in `TESTING` stage. To bypass the warning prompt, add `--quiet` flag.

### Verify

```bash
gcloud iam roles describe simplelinks_network_admin --organization=692154983500
```

---

## Assign a custom role to a user

```bash
gcloud organizations add-iam-policy-binding 692154983500 \
  --member="user:someone@simplelinks.co" \
  --role="organizations/692154983500/roles/ROLE_ID"
```

Replace `ROLE_ID` with `simplelinks_security_viewer` or `simplelinks_network_admin`.

---

## List all custom roles

```bash
gcloud iam roles list --organization=692154983500
```

---

## Delete a custom role

```bash
gcloud iam roles delete ROLE_ID --organization=692154983500
```
