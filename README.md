# Strong-defi-core

This project is the core strong-defi,which also a hardhat template.This is the smart contracts collection of strong-defi project.
so if you want to see any contact,please find it in this project.

the deployment commond is as follows:

1、项目初始化：
```
npm init
npm install --save-dev hardhat
```

2、初始化hardhat,创建一个hardhat项目：
```
yarn hardhat
```

3、添加以太坊相关的依赖：
```
yarn add ethers  @typechain/ethers-v6 @typechain/hardhat @types/chai
```

4、添加环境变量处理及预言机的依赖:
```angular2html
yarn add dotenv
npm install -D @chainlink/contracts
```
5、其他安装依赖包：
```angular2html  
npm install solc@0.8.24  这个是将sol文件编译成,bin，和abi文件的的工具
npm install -D hardhat-deploy  这个插件方便部署合约及测试，文档还需要安装如下的内容：
  1、 npm install --save-dev  @nomicfoundation/hardhat-ethers hardhat-deploy-ethers ethers 安装hardhat-deploy-ethers，方便配合hardhat-deploy一起使用，文档说的
help-hardhat-config,aave-v3-core这个插件可以获取配置的一些模版，给我们提供一个思路
hardhat-gas-reporter，gas-reporter可以查看合约的gas消耗情况，文档：https://www.npmjs.com/package/hardhat-gas-reporter
solidity-coverage ，这个是solidity代码检查的工具。安装命令： yarn add solidity-coverage --dev，具体细节：https://www.npmjs.com/package/solidity-coverage
  1、安装如下命令，因为coverage需要这些包：npm install --save-dev @nomicfoundation/hardhat-chai-matchers@^2.0.0" "@nomicfoundation/hardhat-ignition-ethers@^0.15.0" "@nomicfoundation/hardhat-network-helpers@^1.0.0" "@nomicfoundation/hardhat-verify@^2.0.0" "@types/mocha@>=9.1.0" "hardhat-gas-reporter@^1.0.8" "ts-node@>=8.0.0" "typechain@^8.3.0" "typescript@>=4.5.0
安装@openzeppelin/contracts，这个功能封装了token的协议实现。例如ERC20等。npm install -D @openzeppelin/contracts 
```
 

6、相关运行命令:
```angular2html
1、脚本：yarn hardhat run scripts/deploy.ts 或者  npx hardhat run scripts/deploy.ts  --network [name]
2、编译智能合约命令：npx hardhat compile
3、部署命令：npx hardhat deploy  执行的是deploy包下的所有脚本，按照文件顺序执行
``` 

7、在项目部署前，要先创建.env文件。具体配置可以参考[env.example]，文件中的环境变量如果不需要，需要在config.js中给注释掉，否则会启动会报错
