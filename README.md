# hyperlegder-fabric-chaincode-dev

chaincode  开发流程
1、在chaincode目录开发好go语言代码；
2、启动最简化的容器：
	命令：docker-compose -f docker-compose-simple.yaml up -d

	1个peer
	1个orderer
	1个cli
	1个ccenv

3、编译运行chaincode
	命令：
	    docker exec -it chaincode bash
		编译：go build -o chaincode_example
		运行：CORE_PEER_ADDRESS=peer:7052 CORE_CHAINCODE_ID_NAME=mycc:0 ./chaincode_example
		运行后，进程不要关闭

4、进入cli容器，进行调试
	命令：
		docker exec -it cli bash
		peer chaincode install -p chaincodedev/chaincode/chaincode_example/go -n mycc -v 0
  		peer chaincode instantiate -n mycc -v 0 -c '{"Args":["init","a","100","b","200"]}' -C myc

  		peer chaincode invoke -n mycc -c '{"Args":["invoke","a","b","10"]}' -C myc
  		peer chaincode query -n mycc -c '{"Args":["query","a"]}' -C myc