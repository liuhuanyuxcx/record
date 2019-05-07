# 一、fabric证书工具(cryptogen)和交易工具(configtxgen)的使用  
	#查看证书内容
	openssl x509   -noout -text -in orderer-orderorg.orderorg-cert.pem
    #根据指定的配置文件在指定位置生成证书和密钥
    ../bin/cryptogen generate --config=./crypto-config.yaml --output='crypto-config'
    ../bin/cryptogen generate --config=./crypto-config-test.yaml --output='crypto-config-test'
    生成创世区块
    export FABRIC_CFG_PATH=$PWD
    ../bin/configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block
    将创世区块转换成json
    ../bin/configtxgen -inspectBlock channel-artifacts/genesis.block > genesis_block.json
 