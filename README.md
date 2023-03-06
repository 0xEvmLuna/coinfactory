# CoinAbi

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

## deployContract
```

```
