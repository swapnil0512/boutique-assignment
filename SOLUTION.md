First Error:

Issue: For POD which was in ImagePullBackOff state after deployment for adservice.yaml

Solution: Seems image name which was mentioned in yaml file was not present at mentioned location. So changed the version of image from adservice:v0.3.1 > adservice:v0.3.4. Then applied the changes and was able to deploy the POD successfully.

Before output:
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# kubectl get pods -o wide
NAME                                    READY   STATUS             RESTARTS   AGE    IP            NODE                NOMINATED NODE   READINESS GATES
adservice-78d848d44d-gw2wm              0/1     ImagePullBackOff   0          122m   10.244.1.2    qa-cluster-worker   <none>           <none>
cartservice-c8c9d58cf-pt9bn             0/1     CrashLoopBackOff   41         122m   10.244.1.3    qa-cluster-worker   <none>           <none>
checkoutservice-79dc4c7fb6-5l8k4        1/1     Running            0          122m   10.244.1.4    qa-cluster-worker   <none>           <none>
currencyservice-d6c6fbcbd-qfx6g         1/1     Running            0          122m   10.244.1.5    qa-cluster-worker   <none>           <none>
emailservice-549fc6dc86-77246           1/1     Running            0          122m   10.244.1.6    qa-cluster-worker   <none>           <none>
frontend-6b4d599649-ktjzh               1/1     Running            0          122m   10.244.1.7    qa-cluster-worker   <none>           <none>
paymentservice-7b64f64758-z6qhg         1/1     Running            0          122m   10.244.1.8    qa-cluster-worker   <none>           <none>
productcatalogservice-d6b8696f8-wqm8c   1/1     Running            0          122m   10.244.1.9    qa-cluster-worker   <none>           <none>
redis-cart-85c9fb8bd4-bktzl             0/1     Pending            0          122m   <none>        <none>              <none>           <none>
shippingservice-5d9f5fc746-t96ws        1/1     Running            0          122m   10.244.1.10   qa-cluster-worker   <none>           <none>
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#

  
After Output:
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# kubectl get pods adservice-f96c966c9-wm66m
NAME                        READY   STATUS    RESTARTS   AGE
adservice-f96c966c9-wm66m   1/1     Running   0          58m
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
  
  
Second Error:
 
Issue : For POD which was in CrashLoopBackOff  state after deployment for adservice.yaml
  
Solution: As POD were going into CrashLoopBackOFF state again and again . This issue was due to periodSeconds parameter which was having value less than initialDelaySeconds. So changed parameter of periodSeconds greater than initialDelaySeconds.
  
Before Output:
  
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# kubectl get pods -o wide
NAME                                    READY   STATUS             RESTARTS   AGE    IP            NODE                NOMINATED NODE   READINESS GATES
adservice-78d848d44d-gw2wm              0/1     ImagePullBackOff   0          122m   10.244.1.2    qa-cluster-worker   <none>           <none>
cartservice-c8c9d58cf-pt9bn             0/1     CrashLoopBackOff   41         122m   10.244.1.3    qa-cluster-worker   <none>           <none>
checkoutservice-79dc4c7fb6-5l8k4        1/1     Running            0          122m   10.244.1.4    qa-cluster-worker   <none>           <none>
currencyservice-d6c6fbcbd-qfx6g         1/1     Running            0          122m   10.244.1.5    qa-cluster-worker   <none>           <none>
emailservice-549fc6dc86-77246           1/1     Running            0          122m   10.244.1.6    qa-cluster-worker   <none>           <none>
frontend-6b4d599649-ktjzh               1/1     Running            0          122m   10.244.1.7    qa-cluster-worker   <none>           <none>
paymentservice-7b64f64758-z6qhg         1/1     Running            0          122m   10.244.1.8    qa-cluster-worker   <none>           <none>
productcatalogservice-d6b8696f8-wqm8c   1/1     Running            0          122m   10.244.1.9    qa-cluster-worker   <none>           <none>
redis-cart-85c9fb8bd4-bktzl             0/1     Pending            0          122m   <none>        <none>              <none>           <none>
shippingservice-5d9f5fc746-t96ws        1/1     Running            0          122m   10.244.1.10   qa-cluster-worker   <none>           <none>
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
  
After Output:
  
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# kubectl get pods cartservice-85c5ff6648-npsb2
NAME                           READY   STATUS    RESTARTS   AGE
cartservice-85c5ff6648-npsb2   1/1     Running   7          50m
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
  
Recent all PODS are in running state.
  
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
adservice-f96c966c9-wm66m               1/1     Running   0          62m
cartservice-85c5ff6648-npsb2            1/1     Running   7          51m
checkoutservice-79dc4c7fb6-5l8k4        1/1     Running   0          3h8m
currencyservice-d6c6fbcbd-qfx6g         1/1     Running   0          3h8m
emailservice-549fc6dc86-77246           1/1     Running   0          3h8m
frontend-6b4d599649-ktjzh               1/1     Running   0          3h8m
paymentservice-7b64f64758-z6qhg         1/1     Running   0          3h8m
productcatalogservice-d6b8696f8-wqm8c   1/1     Running   0          3h8m
redis-cart-6ff9d8cc76-tv68z             1/1     Running   0          31m
shippingservice-5d9f5fc746-t96ws        1/1     Running   0          3h8m
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy# date
Tue Aug 16 13:56:29 UTC 2022
root@ip-172-31-9-187:~/test_project/boutique-assignment/deploy#
  
  

