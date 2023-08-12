# Deploy GKE Cluster (CLI)

 export my_zone = us-central1-a
 export my_cluster = standard-cluster-1
 gcloud container clusters create $my_cluster --zone $my_zone --num-nodes 3 --enable-ip-alias

# Modify GKE Cluster 

gcloud container clusters resize $my_cluster --zone $my_zone --num-nodes 4 


# Connect to a GKE Cluster 

gcloud container clusters get-credentials $my_cluster $my_zone

above command creates a .Kube diectory in your home diectory if it doesn't already exists. in the .kube directory the command creates a file name config if it doesn't  already exist, which is used to store the authentication and configuration information.

