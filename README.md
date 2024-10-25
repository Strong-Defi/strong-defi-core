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
npm install solc@0.8.24
npm install -D hardhat-deploy
npm install --save-dev  @nomicfoundation/hardhat-ethers hardhat-deploy-ethers ethers
npm install --save-dev hardhat-gas-reporter
npm install --save-dev solidity-coverage
npm install -D @openzeppelin/contracts 
```
对上面依赖功能的解释：

    1、solc:这个是将sol文件编译成,bin，和abi文件的的工具
    2、hardhat-deploy：这个插件方便部署合约及测试，需要搭配hardhat-ethers，及ethers才可使用，文档：https://hardhat.org/hardhat-runner/plugins/hardhat-deploy
    3、hardhat-gas-reporter：gas-reporter可以查看合约的gas消耗情况，如果不需要，可以不需要安装。文档：https://www.npmjs.com/package/hardhat-gas-reporter
    4、solidity-coverage：这个是solidity代码检查的工具。我一般在remix上写，所以不用，如果在本地写，可以安装这个插件，帮助检查合约的代码。具体细节可查看文档：https://www.npmjs.com/package/solidity-coverage
    5、安装coverage还需要配合其他的依赖，安装如下命令，因为coverage需要这些包：npm install --save-dev @nomicfoundation/hardhat-chai-matchers@^2.0.0" "@nomicfoundation/hardhat-ignition-ethers@^0.15.0" "@nomicfoundation/hardhat-network-helpers@^1.0.0" "@nomicfoundation/hardhat-verify@^2.0.0" "@types/mocha@>=9.1.0" "hardhat-gas-reporter@^1.0.8" "ts-node@>=8.0.0" "typechain@^8.3.0" "typescript@>=4.5.0
    6、@openzeppelin/contracts：这个功能封装了token的协议实现。例如ERC20
    7、npm install -D solc 这个功能是将sol文件编译成abi，bin文件。

6、相关运行命令:
```angular2html
1、脚本：yarn hardhat run scripts/deploy.ts 或者  npx hardhat run scripts/deploy.ts  --network [name]
2、编译智能合约命令：npx hardhat compile
3、部署命令：npx hardhat deploy  执行的是deploy包下的所有脚本，按照文件顺序执行
``` 

7、在项目部署前，要先创建.env文件。具体配置可以参考[env.example]，文件中的环境变量如果不需要，需要在config.js中给注释掉，否则会启动会报错
