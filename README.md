# Deploy GKE Cluster (CLI)

 ``export my_zone = us-central1-a``
 ``export my_cluster = standard-cluster-1``
 ``gcloud container clusters ``create`` $my_cluster --zone $my_zone --num-nodes 3 --enable-ip-alias``

# Modify GKE Cluster 

``gcloud container clusters ``resize`` $my_cluster --zone $my_zone --num-nodes 4 ``


# Connect to a GKE Cluster 

``gcloud container clusters get-credentials $my_cluster $my_zone``

above command creates a .Kube diectory in your home diectory if it doesn't already exists. in the .kube directory the command creates a file name config if it doesn't  already exist, which is used to store the authentication and configuration information.

``vi .kube/config ``

You can now examine all of the authentication and endpoint configuration data stored in the file.

Note:  The kubeconfig file can contain information for many clusters. The currently activie context kubectl commnds manipulate.

``kubectl config view``
``kubectl cluster info``
``kubectl config current-context``
``kubectl config get-contexts ``
``kubectl config use-context < your another cluster name>``  if you have only one cluster didn't change anything

``kubectl top pods ``

``kubectl get quota ``

# use kubectl to deploy pods to GKE

``kubectl create deployment  --image my_nginx nginx-1``

This command creates a Pod name my_nginx  with a container  running the nginx image. `` nginx-1 `` image is comes from either local or public docker registry.

``kubectl get pods``

``kubectl describe pod my_nginx``

If you want to copy files from local to inside  pods  using the below 

``kubectl cp test.html  my_nginx:/usr/share/nginx/html/test.html``


# Expose the Pod for Testing 

TO expose a Pod to clients outside the cluster requires a service.

``kubectl expose pod my_nginx --port 80 --type LoadBalancer``

``kubectl get services (or) svc``

``kubectl logs my_nginx -f --timestamps``










