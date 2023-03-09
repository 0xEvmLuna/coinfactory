<template>
  <el-form :model="formData" ref="vForm" :rules="rules" label-position="top" label-width="80px" size="default"
    @submit.prevent>
    <div class="static-content-item">
      <div>修改营销钱包</div>
    </div>
    <el-form-item label="输入新的营销钱包地址" prop="input70873">
      <el-input v-model="formData.input70873" type="text" clearable></el-input>
    </el-form-item>
    <div class="static-content-item">
      <el-button @click="resetForm">取消</el-button>
    </div>
    <div class="static-content-item">
      <el-button type="primary" @click="submitForm">确认</el-button>
    </div>
  </el-form>
  
</template>

<script>
  import {
    defineComponent,
    toRefs,
    reactive,
    getCurrentInstance
  }
  from 'vue'
  import Web3 from 'web3'
  export default defineComponent({
    components: {},
    props: {},
    setup() {
      const state = reactive({
        formData: {
          input70873: "",
        },
        rules: {},
      })
      const instance = getCurrentInstance()
      const submitForm = () => {
        instance.ctx.$refs['vForm'].validate(async (valid) => {
          if (!valid) return
          //TODO: 提交表单
          const fundAddress = state.formData.input70873
          console.log("fundAddress", fundAddress)

          if (typeof window.ethereum !== 'undefined') {
            try {
              // 请求用户授权
              await window.ethereum.request({ method: 'eth_requestAccounts' });
              // 用户已授权访问账户，执行相关操作
            } catch (error) {
              // 用户未授权访问账户
              console.log(error);
            }
          }


          if (window.web3) {
            window.web3 = new Web3(window.web3.currentProvider);
          } else {
            window.web3 = new Web3(new Web3.providers.HttpProvider('http://localhost:8545'));
          }

          const web3 = window.web3;
          const accounts = await web3.eth.getAccounts();
          const contractAddress = '0x5955ca32370c6Ad85fa68688aBfb5F68b01d7dAa'
          const abi = [{"inputs":[{"internalType":"string[]","name":"stringParams","type":"string]"},{"internalType":"address[]","name":"addressParams","type":"address[]"},{"internalType":"uint256[]","name":"numberParams","type":"uint256[]"},{"internalType":"bool[]","name":"boolParams","type":"bool[]"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"owner","type":"address"},{"indexed":true,"internalType":"address","name":"spender","type":"address"},{"indexed":false,"internalType":"uint256","name":"value","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[],"name":"Failed_addLiquidityETH","type":"event"},{"anonymous":false,"inputs":[],"name":"Failed_swapExactTokensForETHSupportingFeeOnTransferTokens","type":"event"},{"anonymous":false,"inputs":[],"name":"Failed_swapExactTokensForTokensSupportingFeeOnTransferTokens","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"previousOwner","type":"address"},{"indexed":true,"internalType":"address","name":"newOwner","type":"address"}],"name":"OwnershipTransferred","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint256","name":"iterations","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"claims","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"lastProcessedIndex","type":"uint256"},{"indexed":true,"internalType":"bool","name":"automatic","type":"bool"},{"indexed":false,"internalType":"uint256","name":"gas","type":"uint256"},{"indexed":true,"internalType":"address","name":"processor","type":"address"}],"name":"ProcessedDividendTracker","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint256","name":"tokensSwapped","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"amount","type":"uint256"}],"name":"SendDividends","type":"event"},{"anonymous":false,"inputs":[{"indexed":false,"internalType":"uint256","name":"tokensSwapped","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"ethReceived","type":"uint256"},{"indexed":false,"internalType":"uint256","name":"tokensIntoLiqudity","type":"uint256"}],"name":"SwapAndLiquify","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"from","type":"address"},{"indexed":true,"internalType":"address","name":"to","type":"address"},{"indexed":false,"internalType":"uint256","name":"value","type":"uint256"}],"name":"Transfer","type":"event"},{"inputs":[],"name":"ETH","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"_feeWhiteList","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"_mainPair","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"_rewardList","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"","type":"address"}],"name":"_swapPairList","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"_swapRouter","outputs":[{"internalType":"contract IUniswapV2Router02","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"_swapRouterAddress","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"airdropNumbs","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"owner","type":"address"},{"internalType":"address","name":"spender","type":"address"}],"name":"allowance","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"spender","type":"address"},{"internalType":"uint256","name":"amount","type":"uint256"}],"name":"approve","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"balanceOf","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"buy_ETHRewardsFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"buy_burnFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"buy_liquidityFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"buy_marketingFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"buy_totalFees","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"_buyamount","type":"uint256"},{"internalType":"uint256","name":"_sellamount","type":"uint256"}],"name":"changeSwapLimit","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"_amount","type":"uint256"}],"name":"changeWalletLimit","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"claim","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256[]","name":"customs","type":"uint256[]"}],"name":"completeCustoms","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"deadWallet","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"decimals","outputs":[{"internalType":"uint8","name":"","type":"uint8"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"spender","type":"address"},{"internalType":"uint256","name":"subtractedValue","type":"uint256"}],"name":"decreaseAllowance","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"disableChangeTax","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"disableSwapLimit","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"disableWalletLimit","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"dividendTracker","outputs":[{"internalType":"contract ETHBackDividendTracker","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableChangeTax","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableKillBlock","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableOffTrade","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableRewardList","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableSwapLimit","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableTransferFee","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"enableWalletLimit","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"excludeFromDividends","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"fundAddress","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"gasForProcessing","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"spender","type":"address"},{"internalType":"uint256","name":"addedValue","type":"uint256"}],"name":"increaseAllowance","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"isLaunch","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"account","type":"address"}],"name":"isReward","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"kb","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"launch","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"maxBuyAmount","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"maxSellAmount","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"maxWalletAmount","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address[]","name":"addresses","type":"address[]"},{"internalType":"bool","name":"value","type":"bool"}],"name":"multi_bclist","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"mushHoldNum","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"name","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"owner","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"gas","type":"uint256"}],"name":"processDividendTracker","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"renounceOwnership","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"sell_ETHRewardsFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"sell_burnFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"sell_liquidityFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"sell_marketingFee","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"sell_totalFees","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"uint256","name":"newValue","type":"uint256"}],"name":"setAirdropNumbs","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"bool","name":"status","type":"bool"}],"name":"setEnableTransferFee","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address[]","name":"addr","type":"address[]"},{"internalType":"bool","name":"enable","type":"bool"}],"name":"setFeeWhiteList","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address payable","name":"wallet","type":"address"}],"name":"setFundAddress","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"killBlockNumber","type":"uint256"}],"name":"setKillBlock","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"bool","name":"status","type":"bool"}],"name":"setSwapAndLiquifyEnabled","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"addr","type":"address"},{"internalType":"bool","name":"enable","type":"bool"}],"name":"setSwapPairList","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"uint256","name":"newValue","type":"uint256"}],"name":"setSwapTokensAtAmount","outputs":[],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"startTradeBlock","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"swapAndLiquifyEnabled","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"swapTokensAtAmount","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"symbol","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"totalSupply","outputs":[{"internalType":"uint256","name":"","type":"uint256"}],"stateMutability":"view","type":"function"},{"inputs":[{"internalType":"address","name":"recipient","type":"address"},{"internalType":"uint256","name":"amount","type":"uint256"}],"name":"transfer","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"sender","type":"address"},{"internalType":"address","name":"recipient","type":"address"},{"internalType":"uint256","name":"amount","type":"uint256"}],"name":"transferFrom","outputs":[{"internalType":"bool","name":"","type":"bool"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[{"internalType":"address","name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"stateMutability":"nonpayable","type":"function"},{"stateMutability":"payable","type":"receive"}]
          
          // 初始化合约实例
          const contract = new web3.eth.Contract(abi, contractAddress)
          // 合约调用
          // 设置营销钱包
          const txHash = contract.methods.setFundAddress(fundAddress).send({ from: accounts[0] });
          txHash.then((receipt) => {
            console.log(receipt);
          }).catch((error) => {
            console.error(error);
          });
        })
      }
      const resetForm = () => {
        instance.ctx.$refs['vForm'].resetFields()
      }
      return {
        ...toRefs(state),
        submitForm,
        resetForm
      }
    }
  })
  
</script>

<style lang="scss">
  .el-input-number.full-width-input,
  .el-cascader.full-width-input {
    width: 100% !important;
  }
  
  .el-form-item--medium {
    .el-radio {
      line-height: 36px !important;
    }
    
    .el-rate {
      margin-top: 8px;
    }
  }
  
  .el-form-item--small {
    .el-radio {
      line-height: 32px !important;
    }
    
    .el-rate {
      margin-top: 6px;
    }
  }
  
  .el-form-item--mini {
    .el-radio {
      line-height: 28px !important;
    }
    
    .el-rate {
      margin-top: 4px;
    }
  }
  
  .clear-fix:before,
  .clear-fix:after {
    display: table;
    content: "";
  }
  
  .clear-fix:after {
    clear: both;
  }
  
  .float-right {
    float: right;
  }
  
</style>

<style lang="scss" scoped>
  div.table-container {
    table.table-layout {
      width: 100%;
      table-layout: fixed;
      border-collapse: collapse;

      td.table-cell {
        display: table-cell;
        height: 36px;
        border: 1px solid #e1e2e3;
      }
    }
  }
  
  div.tab-container {}
  
  .label-left-align :deep(.el-form-item__label) {
    text-align: left;
  }
  
  .label-center-align :deep(.el-form-item__label) {
    text-align: center;
  }
  
  .label-right-align :deep(.el-form-item__label) {
    text-align: right;
  }
  
  .custom-label {}
  
  .static-content-item {
    min-height: 20px;
    display: flex;
    align-items: center;

    :deep(.el-divider--horizontal) {
      margin: 0;
    }
  }
  
</style>
