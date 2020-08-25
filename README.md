# Kubernetes_Helm
# Building  a single helm chart that can use values for configuration. This helm chart will deploy two services, one will be a simple hello world web server and the other will be a nginx service that will act as a proxy to hello world.
README:- 
Install Kubernetes
Install helm
Install minicube

1) $ helm create hello-world # Hello world folder will be created with various files in it
2) $ vi values.yaml # open file  and enter
replicateCount: 1
Repository: "paulbouwer/hello-kubernetes"
tag: "1:8"
service: 
 type: NodePort
 port: 80
3) $ helm install hello-world hello-world/ --values hello-world/values.yaml
4) $ commmand Kubectl get all # Helm will make the deployment, replicaset, service and corresponding pod automatically
5) $ export POD_NAME=$(kubectl get pods -l "app.kubernetes.io/name=hello-world,app.kubernetes.io/instance=hello-world" -o jsonpath="{.items[0].metadata.name}") # to check the port 
6) kubernetes will run on minicube ip and at port 31391 at localhost.
7) $ cd hello-world\charts
8) $ helm create nginx #  to setting nginx as proxy
9) $ vi value. yml # in ngnix folder 
 enter repository: nginx
       tag : "latest"
       service: 
       type: NodePort
       port: 80

10) go to deployment file 
    enter near the resources 
       volumeMounts:
          - name: nginx-conf
            mountpath: /etc/nginx
            readOnly: true
        
      volumes:
      - name: nginx-conf
        configMap:
           name: nginx-conf
           items:
              - key: nginx.conf
11) create a file configmap.yaml #  mention kind, metadata, data, port.
12) $ helm install nginx nginx/ --values nginx/values.yaml
13) $ kubernetes will run on minicube ip and at port 30081 at localhost.

