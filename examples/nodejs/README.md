### Example: Node.js with hot-reload

Simple example based on Node.js demonstrating the file synchronization mode.

#### Init

```bash
skaffold dev
```

#### Workflow

* Make some changes to `index.js`:
    * The file will be synchronized to the cluster
    * `nodemon` will restart the application
* Make some changes to `package.json`:
    * The full build/push/deploy process will be triggered, fetching dependencies from `npm`


Using OpenShift internal registry doesn't work as the Pod must reference the internal hostanme image-registry.openshift-image-registry.svc:5000.
Easier way is to use external registry:
1. `skaffold config set default-repo quay.io/csantanapr`
2. `oc create secret docker-registry regcred --docker-username=csantanapr --docker-password=‘<PASSWORD>’ --docker-server=quay.io`
3. Add regcred secret as pull secret to service account (ie default)
Replace `csatanapr` with your quay account