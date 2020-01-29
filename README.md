# Cloud Prototyping 2019/2020



#A benchmarking-based approach to maximize throughput of the private Ethereum


Our goals were to achieve :
1) Performance Benchmarking. Benchmarking the performance of private Ethereum with Proof-of-Authority consensus  while maximizing Throughput depending on Block size and Block interval. 
2) Automation. Scaling dynamically the SUT and to derive and present a few high-level guidelines reducing the complexity of implementing and running blockchain benchmarking performance, which would be valuable to developers and deployment engineers.


## Our repository
```
.
├── bin
│   ├── main.py
│   ├── sut
│   │   ├── automated-genesis
│   │   ├── deploy-sut.sh
│   │   ├── startup-script.sh
│   │   └──create-template.sh
│   │   
│   ├── workload
│   │   ├── caliper-config
│   │   ├── caliper-reports
│   │   ├── run-caliper.py
│   │   └── run-caliper.sh
│   │   
│   └── analyzer
│       ├── old
│       ├── aggregated-results
│       ├── aggregate-html-reports.py
│       ├── backup-old-results.py
│       ├── calculate-optimal-values.py
│       └── get-last-throughput
│── config
│      └── config.json
│      
│──  documentation
└──README.md
      
         
```



##Getting started

These instruction will get you a copy of the project up and running on your local machine for development and testing purposes.

git clone https://github.com/Cloud-Prototyping-WS-2019-20/cp_ws_1920.git


##Prerequisites

The script checks if the needed dependencies are installed or how to install them. It also runs the script  create-template.sh  to create VM templates.

Run: sh prerequisites.sh


Dependency
Python libraries : pandas, lxml, matplotlib, numpy
Google SDK
Geth
Puppeth
jq-command
npm (Node.js)
Caliper
 

Note: If you have jq,npm, geth, puppeth and gcloud not installed, you will be provided with the links to follow the easy steps of installing them. This script does not provide their installation, because each user have different OS, and you need to download and install the packages depending on the enviroment you are working from.


##Starting the tool

cd cp_ws_1920/bin
python main.py


##Config (TO-Be-Discussed)

config.json has its objects read by the scripts main.py , deploy-sut.sh , create-template.sh and run-caliper.py .

USERNAME is needed for the authentication when computing ssh.
PASSWORD is needed for the authentication as well, when new accounts on nodes are created.
Network_ID to verify the network we are setting the nodes.

###Under "eth_param" we have:

"templateName", which names the VM instances when they are created. It will be called by bin/sut/create-template.sh
"nodeNumber", when building SUT for the first time, we need at least 2 nodes to set-up private Ethereum on Google Cloud Platform


###The values of "test_param" are all needed to run the main.py.
 
"maxGas" sets the maximal gas limit. Our tool aims to set a range for the minimal and maximal gas limit, where depending on the block interval range we give the optimal throughput to the user.

"defaultGas" we set the default gas to make the mining possible, and define the range of min-max block interval

"gasStep" we add it with the default gas limit we set to search until we find the best minimal value of gas limit, which is needed to do the transactions in the block.

"maxInterval" sets the maximal block interval. Our tool aims to set a range for the minimal and maximal block interval, where depending on the gas limit range we give the optimal throughput to the user.

"intervalStep" we add it with the default block  interval needed to create new block intervals until we find the minimum block interval.
	
###"run_caliper" is read by run-caliper.py.
"attempt" sets the max attempts to run caliper.
		
		
		
##Documentation
This file serves the user to have a more in depth-learning of this tool and how it was organised and developed by the team.


