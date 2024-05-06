# TSBS:

## Setup:
For the comparison of the two databases we utilized the [Time Series Benchmark Suite](https://github.com/timescale/tsbs) for both data generation and insertion and for the batch-queries' generation and execution. In particular, its 'Dev ops' use case, as it is the only "compatible" one with CrateDB. In the hyperlink above, one can find (setup) instructions for TSBS, which we also relied on.

### Go Programming Language Installation:
For the successful installation of TSBS, we were required to have the Go Programming Language installed. To this end, we download (via wget) the necessary compressed file and unzip it (while also ensuring that Go isn't already installed in our system):
```bash
wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz
```
Subsequently, we modify the environment variable PATH in the $HOME/.profile as to include the go/bin:
```bash
export PATH=$PATH:/usr/local/go/bin
```
and apply the changes by executing:
```bash
source $HOME/.profile
```
> To verify that Go is successfully installed, we can execute `go version`

> [!NOTE]
> Before installing TSBS, as refered in the TSBS's instructions, we needed to execute the following command:
> ```bash
> go env -w GO111MODULE=off
> ```
> Once we successfully install TSBS we can re-activate the module we deactivated with the above command, as follows:
> ```bash
> go env -w GO111MODULE=on
> ```

## Data generation & insertion and queries' generation & execution:
For data generation and insertion and for the batch-queries' generation and execution we followed the steps mentioned in TSBS's instuctions. The queries we selected for the project, i.e. those we considered most valuable for a thorough comparison of the two databases, can be found in the [TSBS Queries directory](/Queries/TSBS_Queries), amongst some single-queries of our own making.
