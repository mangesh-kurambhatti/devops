## Deployment


- Represents the logical deployment of a application
- Internally it uses replica set to replicate the pods
- Can be updated or rollbacked using rollback commands

#### Note:

- The main difference between a ReplicaSet and a Deployment is how updates are managed:
  - **ReplicaSet**: Updates (like changing the image version) require you to manually delete and recreate the ReplicaSet. It does not support rolling updates or automated changes at runtime.
  - **Deployment**: Provides automated management for ReplicaSets, including rolling updates, rollbacks, and easier application updates without downtime.

> **Tip:** Deployments are the recommended way to manage stateless applications in Kubernetes because they offer more features and automation than using ReplicaSets directly.


```bash
#get the list of deployments

> kubectl get deployments
OR
> kubectl get deploy

#Decribe deployment
> kubectl describe deployment <deployment-name>

#delete the deployment 
> kubectl delete deploy my-deployment -n ns1
```

### Test Deployments with below steps :

1. Create a deployment with scripr : [deployment](./deployments1.yaml)
2. Run below command to create deployment
    `kubectl apply -f deployments1.yaml`
3. Get all details with below command :
    `kubectl get all -n ns1`

    ```bash
    > ubuntu@master:~/projects/app9-deployments$ kubectl get all -n ns1
        NAME                                READY   STATUS    RESTARTS   AGE
        pod/my-deployment-877bb898d-2p9ph   1/1     Running   0          39s
        pod/my-deployment-877bb898d-9lfng   1/1     Running   0          39s
        pod/my-deployment-877bb898d-n52qq   1/1     Running   0          39s

        NAME                            READY   UP-TO-DATE   AVAILABLE   AGE
        deployment.apps/my-deployment   3/3     3            3           39s

        NAME                                      DESIRED   CURRENT   READY   AGE
        replicaset.apps/my-deployment-877bb898d   3         3         3       39s

    ```

> - Here we can see 3 pods created
> - Deployment created
> - Internally replica set is also created

