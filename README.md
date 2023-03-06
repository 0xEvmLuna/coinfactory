# call examples

## transferOwnership
```
async transferOwnership() {
        try {
          const contractAddress = '0x120....'; // 合约地址
          const contractABI = [...]
          const web3 = new Web3((window as any).ethereum);
          const contractInstance = new web3.eth.Contract(contractABI, contractAddress);
          const fromAddress = '0xfsfa...'; // 当前账户地址
          const toAddress = '0xarb....'; // 接收者地址
          await contractInstance.methods.transferOwnership(toAddress).send({ from: fromAddress });
          console.log('Ownership transfer completed');
        } catch (error) {
          console.error(error);
        }
      } 
```

# deploy Contract
```
import Web3 from "web3";
import Contract from "web3/eth/contract";

// 定义智能合约 ABI 和 bytecode
const contractABI = [{ ... }];
const contractBytecode = "0x...";

export default {
  data() {
    return {
      contractAddress: "",
      web3: null as Web3 | null,
      contract: null as Contract | null,
      account: "",
    };
  },
  async mounted() {
    // 初始化 web3 对象
    const provider = (window as any).ethereum;
    if (provider) {
      this.web3 = new Web3(provider);
      try {
        // 请求用户授权
        await provider.enable();
        // 获取用户账户
        const accounts = await this.web3.eth.getAccounts();
        this.account = accounts[0];
      } catch (error) {
        console.error("User denied account access");
      }
    } else {
      console.error("No provider found");
    }
    // 初始化智能合约对象
    this.contract = new this.web3.eth.Contract(contractABI);
  },
  methods: {
    async deployContract() {
      // 获取智能合约部署参数
      const options = { from: this.account, gas: 5000000, data: contractBytecode };
      // 部署智能合约
      const newContract = await this.contract?.deploy(options).send();
      // 获取合约地址并保存
      this.contractAddress = newContract.options.address;
    },
  },
};

```
