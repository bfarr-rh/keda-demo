# keda-demo
Demo showing scaling with Keda in OpenShift

This is a demo which deploys AMQ-Broker and OpenShift Custom Metrics Autoscaler based on KEDA 

It establishes a broker with 2 queues q1 & q2 and scales a deployment. In this case the deployment is not related to the queue we are merely showing how keda behaves scaling a workload.
The deployment used is pacman but this can be adjusted as required.

Once setup you can send a message to either queue via the Fuse broker console and the scaling will kick in. 

To set up the demo
1. Install the AMQ Broker Operator
2. oc new-project keda-demo
3. Install the custom metrics Operator in the keda-demo project 
4. Install the broker and queues
   oc project keda-demo
   oc apply -f https://raw.githubusercontent.com/bfarr-rh/keda-demo/master/yaml/amq-broker.yaml
5. Create the application
   oc new-app https://github.com/redhat-gpte-devopsautomation/pacman-1
6. Expose the application as a route and test Pacman runs
7. Create the Scaler Object 
   oc apply -f https://raw.githubusercontent.com/bfarr-rh/keda-demo/master/yaml/keda.yaml
8. Navigate to the Fuse console (find the route) and login with admin/admin and use it to send and delete messages from either queue and watch the pods dynamically scale.
