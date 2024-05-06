# QuestDB Setup:
QuestDB is not a distributed database and requires, therefore, a single-node installation. To this end, we execute the following wget command to download the tar file  containing the necessary files (directly from the internet via HTTP/HTTPS), that can be found in it's GitHub repository, which we then extract:
```bash
wget https://github.com/questdb/questdb/releases/download/7.3.7/questdb-7.3.7rt-linux-amd64.tar.gz
tar -xvf questdb-7.3.7-rt-linux-amd64.tar.gz
```
We, subsequently, execute the following command in the directory where the _questdb.sh_ shell file is found to start the database:
```bash
./questdb.sh start
```
With the commands `./questdb.sh stop` and `./questdb.sh status` we can also stop and see the status of the database, respectively.

Using `flag -d`, we can "index" to the root directory of QuestDB. Thus, the default root directory of QuestDB being `HOME/.questdb`, where conf directory is located, that contains, amongst others, QuestDB's configuration file [server.conf](./server.conf).

## Admin UI
We can access the Admin UI of QuestDB via http://localhost:9000, yet a connection using SSH tunneling might be necessary, as explained in the [Important notice in CrateDB's Setup](/CrateDB/README.md/#custom_anchor_name)
