# CrateDB Setup:
As a distributed database, CrateDB requires multi-node setup. For this purpose, we, initially, install CrateDB in all hosts of our system with a single-node setup, modifying subsequently it's "main" configuration file to convert it to a multi-node one.

## Single-node Setup:
To begin with, we ensure that the Advanced Packaging Tool (apt) of Ubuntu  is updated and that all it's required packages are installed, as follows:
```bash
sudo apt update
sudo apt install --yes apt-transport-https apt-utils curl gnupg lsb-release
```
Next, we download the public GPG key, for the OS to authenticate the CrateDB files once we request it's installation:
```bash
curl -sS https://cdn.crate.io/downloads/deb/DEB-GPG-KEY-crate | sudo tee /etc/apt/trusted.gpg.d/cratedb.asc
```
We locate the repository that contains CrateDB and we include it to the list of our system's repositories of package manager apt, as follows:
```bash
[[ $(lsb_release --id --short) = "Debian" ]] &&repository="apt"
[[ $(lsb_release --id --short) = "Ubuntu" ]] &&repository="deb"
distribution=$(lsb_release --codename --short)

echo "deb [signed-by=/etc/apt/trusted.gpg.d/cratedb.asc arch=amd64] https://cdn.crate.io/downloads/${repository}/stable/ ${distribution} main" \
| sudo tee /etc/apt/sources.list.d/cratedb.list
```
At this point, the apt will have access to the reporitories' packages of CrateDB and our system's files (cratedb.list, cratedb.asc) will have all the necessary information for the CrateDB to be installed and hosted in the node through the package manager apt, using the following commands:
```bash
sudo apt update
sudo apt install crate
```
**!** As mentioned earlier, the abovementioned process must be executed in every node of our cluster. We can verify the successful installation of CrateDB by executing the following:
```bash
sudo systemctl start crate # start the database
sudo systemctl stop crate # stop the database
sudo systemctl restart crate # restart the DB
sudo systemctl status crate # check the status of the DB
```
One can alter any desired or/and necessary environment variables in /etc/default/crate. We opted for the following:
```bash
CRATE_HEAP_SIZE=2g
MAX_LOCKED_MEMORY=unlimited
CRATE_USE_IPV4=true
```
## Multi-node Setup:
At this point, the single-node installation is completed and we can proceed to the necessary configuration for a multi-node (cluster) setup of CrateDB. We modify each node's [crate.yml file](./crate.yml), that can be found in the /etc/crate directory, as follows:
- For each node to be "visible" and connect with the others:
  ```bash
  discovery.seed hosts :
  − 192.168.1.2:4300
  − 192.168.1.3:4300
  − 192.168.1.4:4300
  ```
- For nodes to know which ones participate in the election of the master-node during the first bootstrapping of the system (we considered all nodes eligible to become master-node):
  ```bash
  cluster . initial master nodes :
  − 192.168.1.2
  − 192.168.1.3
  − 192.168.1.4
  ```
- To inform the database of the number of data-nodes expected, as well as the number of nodes that should be "alive" before attempting recovery (with the following options we essentially prevent the database from rebalancing if some node fails, since, for this project, we consider that every node recovers shortly):
  ```bash
  gateway:
        recover_after_data_nodes: 3
        expected_data_nodes: 3
  ```
- To specify to which IP adddresses CrateDB will "bind" (by setting it to 0.0.0.0, we allow CrateDB to listen on all network interfaces for incoming requests), as well as for each node to publish to the rest of the cluster the address through which IP they can communicate (in each node's file this should have its private IP address):
  ```bash
  network.bind_host: 0.0.0.0
  network.publish_host: 192.168.1.2
  # or 192.168.1.3 or 192.168.1.4
  # (depends on the current node)
- To define the cluster's (optional) and each node's name:
  ```bash
  cluster.name: my_cluster
  node.name: <node-name>
  ```
  where node-name in our setup: okeanos-ISmaster or okeanos-ISworked1 or okeanos-ISworker2, depending on the node, whose configuration file we are in.

At this point, CrateDB can run in the cluster of the system's nodes and we can start it by executing `sudo systemctl start crate` in each node.

## Admin UI:
After the completion of either the single-node or the multi-node setup and having started the database, one can access the Admin UI of CrateDB in http://localhost:4200/.
<a name="custom_anchor_name"></a>
> [!IMPORTANT]  
> In the case that the user (in this case, ourselves) is using their local machine while the cluster is running on VMs (e.g. of okeanos), in order to gain access to the Admin UI via localhost, it is necessary to use SSH tunneling during the connection process (from the local machine) to one of the remote nodes of the CrateDB cluster. This enables a secure, encrypted transfer of traffic to port 4200 (where CrateDB is running) on the remote machine to the corresponding port on the local machine. The "-i" argument specifies the directory where the private key, that was initially created, is stored, allowing the connection to be established in an authorized manner:
> ```bash
> ssh -i ∼/.ssh/id_rsa -L 4200:localhost:4200 user@snf-39924.ok-kno.grnetcloud.net
> ``` 
