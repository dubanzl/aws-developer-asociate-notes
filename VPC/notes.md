| Subnet Type                 | Route Table Rule                     | Internet Access          | Typical Resources                          | Key Idea to Remember                      |
| --------------------------- | ------------------------------------ | ------------------------ | ------------------------------------------ | ----------------------------------------- |
| **Public Subnet**           | `0.0.0.0/0 → Internet Gateway (IGW)` | ✅ Direct Internet access | Web servers, load balancers, bastion hosts | Route table sends traffic to **IGW**      |
| **Private Subnet**          | No route to IGW                      | ❌ No Internet access     | Databases, internal services               | Completely isolated from Internet         |
| **Private Subnet with NAT** | `0.0.0.0/0 → NAT Gateway`            | ✅ Outbound only          | Application servers, backend services      | Can **reach Internet but not be reached** |


| Component            | Role                                                   |
| -------------------- | ------------------------------------------------------ |
| **VPC**              | The entire network                                     |
| **Subnet**           | A smaller section of the network                       |
| **Route Table**      | Decides where traffic goes                             |
| **Internet Gateway** | Allows Internet access                                 |
| **NAT Gateway**      | Allows **outbound-only Internet** from private subnets |


Internet
   │
   ▼
Internet Gateway
   │
   ▼
PUBLIC SUBNET
(Web servers, ALB)
   │
   ▼
NAT Gateway
   │
   ▼
PRIVATE SUBNET
(App servers)
   │
   ▼
PRIVATE SUBNET
(Database)


----
Configure VPC endpoints for DynamoDB that will provide required internal access without using public internet



On-premises network
        │
        │ BGP VPN
        │
AWS VPC
   ├─ Subnet A
   └─ Subnet B


   | Technology              | Purpose                  |
| ----------------------- | ------------------------ |
| BGP                     | exchanges network routes |
| VPN                     | encrypted tunnel         |
| VPC Flow Logs           | shows network traffic    |
| Security Groups / NACLs | allow or block traffic   |
