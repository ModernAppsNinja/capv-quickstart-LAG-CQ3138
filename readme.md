# ClusterAPI Provider for vSphere Quickstart 

**Contents:**

- [Pre-Requisites](#pre-requisites)
- [Step 1: Install CAPV Image](#step-1-install-capv-image)
- [Step 2: Configure CAPV Image](#step-2-configure-capv-image)
- [Step 3: Install and Connect Octant](step-3-install-and-connect-octant)
- [Step 4: Review CAPV Configuration Script](#step-4-review-capv-configuration-script)
- [Step 5: Review ClusterAPI Manifests & vCenter Deployment](#step-5-review-clusterapi-manifests-vcenter-deployment)
- [Next Steps](#next-steps)

## Pre-Requisites

- Pre.1 Requires a vSphere environment of 6.7U3 or better. DHCP is a requirement as well. Make sure there is a functioning DHCP service. 
- Pre.2 Required Lab Environment - PKS-Ninja-T1-Baseline (see validate.md for specific labEnvironment versions validated for this guide)

## Step 1: Install CAPV Image

1.1 From the Control Center Desktop,  Download the CAPV image from the [CAPV Github Repo](https://github.com/kubernetes-sigs/cluster-api-provider-vsphere#kubernetes-versions-with-published-ovas). At the time of this writing, this example is using Photon 1.16.3

<details><summary>Screenshot 1.1</summary>

</details>
<br/>

1.2	Open a web browser tab to vcenter and login using the Windows system credentials. Right-click on the `RegionA01-COMP01` cluster and select `Deploy OVF Template`

<details><summary>Screenshot 1.2</summary>

</details>
<br/>

1.3	On the `Select an OVF Template` screen, select the CAPV image you downloaded in the previous step

<details><summary>Screenshot 1.3</summary>

</details>
<br/>

1.4	on the `Select a name and folder` page, set the `Virtual Machine Name`

<details><summary>Screenshot 1.3</summary>

</details>
<br/>








---------------------------
1.3	Set the CAPV Image as a Template. Right Click and set as Template

<details><summary>Screenshot 1.3</summary>
![image](https://user-images.githubusercontent.com/60424950/74877766-d79f0700-531a-11ea-800c-f60d50931d4e.png)
</details>
<br/>


## Step 2: Configure CAPV Image

2.1	Instead of following the CAPV QuickStart, we will use a script to automate the deployment. Open an ssh connection to cli-vm to bootstrap cluster

![image](https://user-images.githubusercontent.com/60424950/74878195-aecb4180-531b-11ea-8b15-cdf5d9da8d86.png)


2.2	After the VM has come up, SSH into the virtual machine. Create a new file called `capv.sh` and copy and paste this QuickStart script.

2.3	Run `sudo chmod u+x capv.sh`, then execute with `sudo ./capv.sh`

2.4	The script will prompt for questions as it relates to the vCenter IP, username, password, and other environment variables needed such as the vCenter Datacenter, the VM network to attach the VMs, Resource Pool, Datastore, Folder and so on. Accept the defaults for the remaining unless you feel inclined to change or add additional workers. 

![image](https://user-images.githubusercontent.com/60424950/74878225-bf7bb780-531b-11ea-9b47-e57a69d88340.png)


2.5	The script will do a complete installation of docker, kind, clusterctl, and kubectl. It will then create the vSphere configuration file needed for the CAPV manifests. The Ubuntu VM will initiate a kind bootstrap cluster that will create the management-cluster. After the management cluster is created, the kind bootstrap cluster is removed. The manifests for the workload cluster are generated and then applied to the management cluster. This will begin deploying workload-cluster-1. management-cluster and workload-cluster-1 are default names used. After workload-cluster-1 is online, Calico is applied for networking. 

2.6	the following text is displayed and you can interact with any cluster

```bash
Kubernetes Workload Cluster Deployment is Complete!
Use 'export KUBECONFIG="$(pwd)/out/workload-cluster-1/kubeconfig"' to interact with the workload cluster using kubectl.
Use 'export KUBECONFIG="$(pwd)/out/management-cluster/kubeconfig"' to interact with the management cluster using kubectl.
Access the Octant UI at boot.vsphere.local:7777 or 10.173.61.70:7777
```

## Step 3: Install and Connect Octant

3.1	Lastly, Octant is installed to have a GUI

![image](https://user-images.githubusercontent.com/60424950/74878251-cb677980-531b-11ea-9680-3c424d106630.png)


## Step 4: Review CAPV Configuration Script

4.1 Add Steps

## Step 5: Review ClusterAPI Manifests & vCenter Deployment

5.1 On the Ubuntu VM, go to the `out` directory in the PWD to see the Cluster API manifests that were generated. These can be manipulated and re-applied with kubectl to the respective clusters. You can also look at the script to see how to create a second workload cluster and have that be applied.

![image](https://user-images.githubusercontent.com/60424950/74878284-dde1b300-531b-11ea-8331-32a928b247c1.png)


5.2.	Here's an example of what the vSphere environment will look like

![image](https://user-images.githubusercontent.com/60424950/74878296-e4702a80-531b-11ea-9edd-c5819440e6ab.png)


## Next Steps
Enter Next Steps here
