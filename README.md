# Ensure Failover Clustering feature is installed
Install-WindowsFeature Failover-Clustering -IncludeManagementTools

# Define cluster parameters
$clusterName = "MyCluster"
$nodes = "Node1", "Node2"  # Replace with your node names
$staticIP = "192.168.1.100" # Replace with your desired cluster IP

# Test cluster configuration (optional but recommended)
Test-Cluster -Node $nodes

# Create the cluster
New-Cluster -Name $clusterName -Node $nodes -StaticAddress $staticIP -NoStorage

# Note: The -NoStorage flag is used for this example since we're not configuring shared storage.
# In a real-world scenario, you'd use Add-ClusterSharedVolume to add shared storage after cluster creation.

# Validate the newly created cluster
Get-Cluster -Name $clusterName

# Test cluster validation (optional but recommended)
Test-Cluster -Node $nodes
