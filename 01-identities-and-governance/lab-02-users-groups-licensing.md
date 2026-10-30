## 🚀 LAB 2: Identity Management, Custom Domain Verification, User Provisioning & Dynamic Group Governance

Following the AZ-104 course schedule, **Lab 2** builds directly on the baseline setup from Lab 1 by executing public DNS verification, creating enterprise user identities, and setting up automated group-based licensing.

---

### 📋 Step-by-Step Instructions for Lab 2

#### Step 1: Complete Public DNS Verification for `robinhood305h3a0l5.com`
1. Open [Microsoft Entra Admin Center](https://entra.microsoft.com).
2. Navigate to **Identity** $\rightarrow$ **Settings** $\rightarrow$ **Domain names**.
3. Click on **`robinhood305h3a0l5.com`**.
4. Copied the generated **TXT record details**:
   * **Host / Alias:** `@`
   * **Value:** `MS=msXXXXXXXX` (Copied my unique string)
   * **TTL:** `3600`
5. Logged into my **DNS Registrar** (Namecheap, Cloudflare, GoDaddy, or Azure DNS) (I chose Cloudflare to save $$$).
6. Created a new **TXT Record** using the copied values.
7. Returned to Microsoft Entra Admin Center and click **Verify**.
8. Once verified, I click **Make primary** to set `robinhood305h3a0l5.com` as the primary tenant UPN suffix.

---

#### Step 2: Create Operational User Identities
Create three distinct administrative and technical user accounts using the custom domain suffix:

| Display Name | User Principal Name (UPN) | Usage Location | Directory Role |
| :--- | :--- | :--- | :--- |
| **Hal Knowles (Admin)** | `halknowles@robinhood305h3a0l5.com` | United States | Global Administrator |
| **User Admin Tech** | `usr-admin@robinhood305h3a0l5.com` | United States | User Administrator |
| **Helpdesk Tech** | `helpdesk@robinhood305h3a0l5.com` | United States | Helpdesk Administrator |

1. Go to **Identity** $\rightarrow$ **Users** $\rightarrow$ **All users** $\rightarrow$ **+ New user** $\rightarrow$ **Create new user**.
2. Set the domain suffix dropdown to `@robinhood305h3a0l5.com`.
3. Under **Properties** $\rightarrow$ **Settings**, set **Usage Location** to **United States** *(Required for licensing)*.
4. Set **Department** to `IT`.

---

#### Step 3: Configure Dynamic Security Group & Group-Based Licensing
1. Navigate to **Identity** $\rightarrow$ **Groups** $\rightarrow$ **All groups** $\rightarrow$ **+ New group**.
2. **Group type:** Security
3. **Group name:** `Robinhood305-IT-Staff`
4. **Membership type:** Dynamic User
5. Click **Add dynamic query** and construct the rule:
   ```text
   (user.department -eq "IT")
---

## 🚀 Next Up | Lab 3 Agenda: Enterprise Azure RBAC & Custom Role Definitions

With tenant-level identities active, **Lab 3** transitions to resource-level access governance using **Azure Role-Based Access Control (RBAC)**:

- 🔹 **Built-in Role Delegation:** Assigning targeted `Contributor` access over resource groups under least-privilege principles.
- 🔹 **Custom JSON Role Creation:** Deploying a custom `Virtual Machine Operator` role to allow starting/stopping VMs without full management access.
- 🔹 **Scope Inheritance Verification:** Validating permission inheritance across Subscription $\rightarrow$ Resource Group $\rightarrow$ Resource levels.
- 🔹 **Access Control Testing:** Verifying that unauthorized resource creation attempts are explicitly denied by Azure IAM policies.
