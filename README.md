# Tailscale Exit Node VPN

A cloud-init script to provision a server as a Tailscale exit node for VPN use.

## Setup

### 1. Configure Tailscale Admin Console

1. Go to [Tailscale Admin Console](https://login.tailscale.com/admin/settings/oauth)
2. Create an OAuth client with:
   - `auth_keys` scope (Write)
   - Tag: `tag:vpn`
3. Update your [ACL policy](https://login.tailscale.com/admin/acls) to auto-approve exit nodes:
   ```json
   {
     "tagOwners": {
       "tag:vpn": ["autogroup:admin"]
     },
     "autoApprovers": {
       "exitNode": ["tag:vpn"]
     }
   }
   ```

### 2. Deploy

1. Copy your OAuth client secret into `cloud-init.yaml`
2. Deploy a VM with `cloud-init.yaml` as user data
