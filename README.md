# IMP points about GCP resources


.

🔧 🔑 Summary:

| Feature                | Required? | Purpose                                                               |
| ---------------------- | --------- | --------------------------------------------------------------------- |
| `default-deny-ingress` | Yes       | Blocks all ingress unless explicitly allowed                          |
| Allow IAP to Bastion   | Yes       | To SSH into Bastion via IAP                                           |
| Allow IAP to nginx VM  | Yes       | To SSH into nginx via IAP (if direct access needed)                   |
| Allow Bastion to nginx | Yes       | To SSH from Bastion to nginx (optional if using Bastion as jump host) |


🔒 How GCP Default-Deny Works:
| Direction | Rule Type            | Purpose                      |
| --------- | -------------------- | ---------------------------- |
| Ingress   | default-deny-ingress | Block all ingress by default |
| Egress    | default-allow-egress | Allow all egress by default  |


✅ Final Setup You Need:
| Purpose                      | Firewall Rule                      | Source          | Target Tag |
| ---------------------------- | ---------------------------------- | --------------- | ---------- |
| IAP to Bastion VM            | allow-iap-ssh-bastion              | 35.235.240.0/20 | bastion-vm |
| Bastion VM to nginx VM       | allow-bastion-to-nginx             | bastion-vm      | nginx-vm   |
| Deny All Unspecified Ingress | default-deny-ingress (GCP default) | All             | All VMs    |


