# Infrastructure

## AWS Zones
us-west-1a, us-west-1b
us-east-2a, us-east-2b, us-east-2c

## Servers and Clusters
In each avail region: Two node RDS cluster in each AZ, 2 node cluster in each AZ, 3 Web servers

### Table 1.1 Summary
| Asset         | Purpose                          | Size                 | Qty                           | DR                                                |
|---------------|----------------------------------|----------------------|-------------------------------|---------------------------------------------------|
| Load balancer | Direct Traffic in region         | n/a                  | One load balancer per region  | configuration needs to be duplicated for failover |
| SQL Cluster   | SQL Server Resiliency            | t3.micro             | See DR column                 | primary write/ others read                        |     
| SQL DB Server | Data stored in the database      | db.t3.micro          | 4 db instances                | Replication to 2nd region in real time            |
| Web Server    | Web App/Site                     | t3.micro             | 3 per region                  |                                                   |
| VIP           | Traffic Direction                | ---                  | 1 per AZ                      | VIPS for cluster per region                       |
| Web Cluster   | HA configuration for web app     | t3.medium            | 2 node clusters               | clusters are created in 2 regions                 |

### Descriptions
There is a two node web server cluster with cluster nodes in 2 regions and VM instances in multiple AZs. VIP addresses are each AZ and a load balancer is configured in each region for traffic routing.
SQL is deployed using a two node cluster in two AZs.  An HA primary write instance runs in one region and replicates data to a read cluster (in the other region).  

## DR Plan
### Pre-Steps:
1.  Config the web server cluster with Terraform in the first zone.  After this you can duplicate the config into a the second zone directory and update the AZs
2.  Config the SQL server primary and secondary instances in zone1
3.  Run terraform apply from each zone 

## Steps:
1) Perform a failover for the web servers by using the DNS service for AWS to direct traffic from the public DNS to the load balancer in the secondary region
2) Promote the EKS cluster in the other region
3) Using the RDS Console you will promote the other regions read only copy of the RDS database into the region where the alternate cluster is located