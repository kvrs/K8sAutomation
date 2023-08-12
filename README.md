## Deploy GKE Cluster (CLI)

export my_zone = us-central1-a
export my_cluster = standard-cluster-1
gcloud container clusters create $my_cluster --zone $my_zone --num-nodes 3 --enable-ip-alias

## Modify GKE Cluster 

gcloud container clusters ##resize $my_cluster --zone $my_zone --num-nodes 4 
