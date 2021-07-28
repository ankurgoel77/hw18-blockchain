# HW 18 - Proof of Authority Blockchain
To set up a testnet, first we need to setup some nodes using Geth.  For this setup, Geth is installed in a sister directory called "blockchain_tools".
### Node Configuration
First, we create 2 nodes using geth.  Those commands are:

> ../blockchain_tools/geth --datadir node1 account new  
> ../blockchain_tools/geth --datadir node2 account new

Running these commands will provide us public addresses of the nodes, as well as a file that has the private key.

For these nodes, the files are saved to the repository as:

* Node 1 : [./node1/keystore/UTC--2021-07-22T21-09-56.284893500Z--d8b832d32ac8b331b784a2d9c53e0a3db071d8ff](node1/keystore/UTC--2021-07-22T21-09-56.284893500Z--d8b832d32ac8b331b784a2d9c53e0a3db071d8ff)
* Node 2 : [./node2/keystore/UTC--2021-07-22T21-10-29.386343100Z--ad4d6b27d858bc0f355c5437c1b6d3f58c25b013](node2/keystore/UTC--2021-07-22T21-10-29.386343100Z--ad4d6b27d858bc0f355c5437c1b6d3f58c25b013)

Once the private keys are extracted, they need to be made secret. To help manage these files, I have stored them in the [keys.txt](keys.txt) file for easy referral.

### Blockchain Configuration
Once the nodes are created, we can now use Puppeth to setup our blockchain.
 > ../blockchain_tools/puppeth
 I have screenshots of the configuration as follows:  

![Puppeth screen 1](Screenshots/puppeth1.PNG)
![Puppeth screen 2](Screenshots/puppeth2.png)

This sets up a Proof of Authority blockchain using the 2 nodes we setup previously, and both nodes are allowed to approve any transactions.  Note that both nodes are pre-funded.

### Blockchain Startup
Now that the blockchain is created, we need to start it up.  We will need 2 terminals, as the blockchains will run continuously in the foreground.  

For the first node, run:
> ../blockchain_tools/geth --datadir node1 --unlock "0xd8b832d32ac8b331b784a2d9c53e0a3db071d8ff" --mine --rpc --allow-insecure-unlock

This will start up a mining node as follows:
![Mining Node 1](Screenshots/run_node1.PNG)

We need to copy the enode from this mining block as   
* enode://e1139601f27b942205a425d8c222a45d30fd10f6dbcc5c910d040e804d2ea6729d3373e4db99573b7675723349dc520d2ba1ec3cf5b1c963cd30e64ea3accec3@68.170.95.241:30303  

We can then run the 2nd node in another terminal:

> ../blockchain_tools/geth --datadir node2 --unlock "0xad4d6b27d858bc0f355c5437c1b6d3f58c25b013" --mine --port 30304 --bootnodes "enode://e1139601f27b942205a425d8c222a45d30fd10f6dbcc5c910d040e804d2ea6729d3373e4db99573b7675723349dc520d2ba1ec3cf5b1c963cd30e64ea3accec3@68.170.95.241:30303" --ipcdisable --allow-insecure-unlock

This will start up a second node as follows:
![Mining Node 2](Screenshots/run_node2.PNG)

The blockchain is up and running!

### Performing Transactions


