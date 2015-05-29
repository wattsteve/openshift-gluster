# openshift-gluster

### Deploy the GlusterFS Container

1) Identify a machine within your OpenShift SDN that will run GlusterFS. Run this command on that machine
 
     # docker run --privileged -d jsafrane/kubernetes-gluster
  
2) Obtain the IP Address that the container is running on

     # docker ps  (This displays the Container ID)
  
     # docker inspect {ContainerID} | grep “IPAddress"

### Configure and Test the GlusterFS Volume Plugin in OSV3

1) Git clone the openshift-gluster test repo 

     # git clone https://github.com/wattsteve/openshift-gluster.git
     
2) Edit the glusterfs-container.json endpoint file and replace the Endpoints IP address with the one retrieved from the GlusterFS container

     # vi  glusterfs-container.json

1) Submit the endpoints file

     # osc create -f glusterfs-container.json 

2) Verify the endpoint was created successfully

     # osc get endpoints

3) Submit the sample nginx web application pod. This will launch an nginx web server that mounts the GlusterFS volume into the NGINX Document Root.

     # osc create -f nginx-pod-gluster.json 

4) Verify the pod is running and get the IP Address of the NGINX Container from the display

     # osc get pods

5) Test the Web Application using the IP address returned from the Pod (this must be run on a machine within the OpenShift SDN)

     # curl {IPAddressOfPod}/test/index.html
