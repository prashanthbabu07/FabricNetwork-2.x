# FabricNetwork-2.x

Youtube Channel: https://www.youtube.com/watch?v=SJTdJt6N6Ow&list=PLSBNVhWU6KjW4qo1RlmR7cvvV8XIILub6


Network Topology

Three Orgs(Peer Orgs)

    - Each Org have one peer(Each Endorsing Peer)
    - Each Org have separate Certificate Authority
    - Each Peer has Current State database as couch db


One Orderer Org

    - Three Orderers
    - One Certificate Authority



Steps:

1) Clone the repo


2) Run Certificates Authority Services for all Orgs
    cd artifacts/channel/create-certificate-with-ca
    docker-compose up -d
    artifacts/channel/create-certificate-with-ca/docker-compose.yaml


3) Create Cryptomaterials for all organizations
    artifacts/channel/create-certificate-with-ca/create-certificate-with-ca.sh

    
4) Create Channel Artifacts using Org MSP
    cd artifacts/channel
    ./create-artifacts.sh

5) Create Channel and join peers
    cd artifacts
    docker-compose up -d
    artifacts/docker-compose.yaml

    createChannel.sh

6) Deploy Chaincode
   1) Install All dependency
   2) Package Chaincode
   3) Install Chaincode on all Endorsing Peer
   4) Approve Chaincode as per Lifecycle Endorsment Policy
   5) Commit Chaincode Defination

    deployChaincode.sh


7) Create Connection Profiles
    cd api-2.0
    npm install

    connection profiles generate
    api-2.0/config/generate-ccp.sh

8) Start API Server
    cd api-2.0
    nodemon app.js
    node app.js

9) Register User using API
    api-2.0/postman-collection/link.txt
    /users
    access couchdb

    http://localhost:5984/_utils
    admin
    adminpw
    

10) Invoke Chaincode Transaction
    channel/mychannel/chaincode/fabcar

11) Query Chaincode Transaction
    channel/mychannel/chaincode/fabcar?fnc=GetCarById


deploy multiple chaincode on same channel
    deployDocumentCC.sh


communicate between channels.
    https://www.youtube.com/watch?v=JL4FsZcY468&list=PLSBNVhWU6KjW4qo1RlmR7cvvV8XIILub6&index=58

    artifacts/src/github.com/fabcar/go/fabcar.go
        GetDocumentUsingCarContract
        CreateDocumentUsingCarContract


deploy multiple smart contract in the same chain code.
    artifacts/src/github.com/multicontracts_cc/go/fabcar.go
    deployMultipleContract.sh

    https://www.youtube.com/watch?v=TZY2Gooh4f8&list=PLSBNVhWU6KjW4qo1RlmR7cvvV8XIILub6&index=59

Smart Contract
    Events -
        artifacts/src/github.com/fabcar/go/fabcar.go    
        Line 46 - raising events.
        Client listener - api-2.0/app/Listeners.js


    Contract Listener
    await contract.addContractListener(contractListener);

    Network Listener
    await network.addBlockListener(blockListener);