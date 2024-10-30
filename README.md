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
4、智能合约编译命令： solcjs --abi --include-path node_modules/ --base-path . contracts/SCHStake.sol -o /Users/v_shaochunhai/Desktop/ether/go_project/strong-defi-backend/abi 
    1、 --include-path node_modules/，表示编译import的合约
    2、 --base-path .，表示编译当前目录下的合约
    3、 -o bin，表示输出abi和bin文件
``` 

7、在项目部署前，要先创建.env文件。具体配置可以参考[env.example]，文件中的环境变量如果不需要，需要在config.js中给注释掉，否则会启动会报错

8、合约介绍
```angular2html
需求文档

1️⃣ 系统概述
SCHStake 是一个基于区块链的质押系统，支持多种代币的质押，并基于用户质押的代币数量和时间长度分配 SCToken 代币作为奖励。系统可提供多个质押池，每个池可以独立配置质押代币、奖励计算等。

2️⃣ 功能需求
2.1 质押功能
输入参数: 池 ID(_pid)，质押数量(_amount)。
前置条件: 用户已授权足够的代币给合约。
后置条件: 用户的质押代币数量增加，池中的总质押代币数量更新。
异常处理: 质押数量低于最小质押要求时拒绝交易。

2.2 解除质押功能
输入参数: 池 ID(_pid)，解除质押数量(_amount)。
前置条件: 用户质押的代币数量足够。
后置条件: 用户的质押代币数量减少，解除质押请求记录，等待锁定期结束后可提取。
异常处理: 如果解除质押数量大于用户质押的数量，交易失败。

2.3 领取奖励
输入参数: 池 ID(_pid)。
前置条件: 有可领取的奖励。
后置条件: 用户领取其奖励，清除已领取的奖励记录。
异常处理: 如果没有可领取的奖励，不执行任何操作。

2.4 添加和更新质押池
输入参数: 质押代币地址(_stTokenAddress)，池权重(_poolWeight)，最小质押金额(_minDepositAmount)，解除质押锁定区(_unstakeLockedBlocks)。
前置条件: 只有管理员可操作。
后置条件: 创建新的质押池或更新现有池的配置。
异常处理: 权限验证失败或输入数据验证失败。

2.5 合约升级和暂停
升级合约: 只有持有升级角色的账户可执行。
暂停/恢复操作: 可以独立控制质押、解除质押、领奖等操作的暂停和恢复。


4️⃣ 安全需求
访问控制: 使用角色基础的访问控制确保只有授权用户可以执行敏感操作。
重入攻击保护: 使用状态锁定模式防止重入攻击。
输入验证: 所有用户输入必须经过严格验证，包括参数范围检查和数据完整性验证。

5️⃣ 事件记录
每个关键操作（如质押、解除质押、领奖）都应触发事件，以便外部监听器跟踪和记录状态变化。

6️⃣ 接口设计
提供标准的 Ethereum 智能合约接口，支持 ERC20 代币操作和自定义合约方法。
提供前端界面调用合约的接口说明和示例代码，确保前端可以正确交互并展示合约状态。

```
