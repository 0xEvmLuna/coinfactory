<template>
  <el-form :model="formData" ref="vForm" :rules="rules" label-position="left" label-width="75px"
    size="default" @submit.prevent>
    <el-form-item label="代币名称" prop="input84916" class="label-center-align">
      <el-input v-model="formData.input84916" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币简称" prop="input3108" class="label-center-align">
      <el-input v-model="formData.input3108" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币精度" prop="input77472" class="label-center-align">
      <el-input v-model="formData.input77472" type="text" placeholder="代币精度一般使用18" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币总量" prop="input34416" class="label-center-align">
      <el-input v-model="formData.input34416" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="选择模板" prop="select85272">
      <el-select v-model="formData.select85272" class="full-width-input" clearable>
        <el-option v-for="(item, index) in select85272Options" :key="index" :label="item.label"
          :value="item.value" :disabled="item.disabled"></el-option>
      </el-select>
    </el-form-item>
    <div class="static-content-item">
      <el-button type="primary" @click="submitForm">创建代币</el-button>
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
          input84916: "",
          input3108: "",
          input77472: "",
          input34416: "",
          select85272: "",
        },
        rules: {
          input34416: [{
            pattern: /^\d+(\.\d+)?$/,
            trigger: ['blur', 'change'],
            message: ''
          }],
          input77472: [{
            pattern: /^\d+(\.\d+)?$/,
            trigger: ['blur', 'change'],
            message: ''
          }],
        },
        select85272Options: [{
          "label": "无税通用模板",
          "value": 1
        }, {
          "label": "无有税通用模板",
          "value": 2
        }, {
          "label": "持币分红模板",
          "value": 3
        }, {
          "value": 4,
          "label": "加池分红模板"
        }],
      })

      const instance = getCurrentInstance()


      const submitForm = () => {
        instance.ctx.$refs['vForm'].validate(async (valid) => {
          if (!valid) return

          //TODO: 提交表单
          if (typeof window.ethereum !== 'undefined') {
            try {
              // 请求用户授权
              await window.ethereum.request({ method: 'eth_requestAccounts' });
              // 用户已授权访问账户，执行相关操作
            } catch (error) {
              // 用户未授权访问账户
              console.error(error);
            }
          }
          
            if (window.web3) {
              window.web3 = new Web3(window.web3.currentProvider);
            } else {
              window.web3 = new Web3(new Web3.providers.HttpProvider('http://localhost:8545'));
            }


            const web3 = window.web3;
            const accounts = await web3.eth.getAccounts();
            const abi = [
                  {
                    "inputs": [],
                    "name": "get",
                    "outputs": [
                      {
                        "internalType": "uint256",
                        "name": "",
                        "type": "uint256"
                      }
                    ],
                    "stateMutability": "view",
                    "type": "function"
                  }
            ];
            const bytecode = '608060405234801561001057600080fd5b5060b68061001f6000396000f3fe6080604052348015600f57600080fd5b506004361060285760003560e01c80636d4ce63c14602d575b600080fd5b60336047565b604051603e91906067565b60405180910390f35b60006001905090565b6000819050919050565b6061816050565b82525050565b6000602082019050607a6000830184605a565b9291505056fea2646970667358221220f88616454f52e0d0f116ceac48732d3b0accaa91e57ab00f9a35440b3d3e7c8664736f6c63430008120033'
            const contract = new web3.eth.Contract(abi);
            const deployedContract = await contract.deploy({
              data: bytecode,
              arguments: []
            }).send({
              from: accounts[0],
              gas: '5000000',
            }, (error, transactionHash) => {
              if (error) {
                console.error(error);
              } else {
                console.log(transactionHash);
              }
            })


            // 在区块链浏览器中验证
            const sourceCode = await web3.eth.getCode(deployedContract.options.address);
            const data = {
              apikey: 'CIFMXUC696VIJ1RZ3FERDUK3YKVT88JWKP',
              module: 'contract',
              action: 'verifysourcecode',
              contractaddress: deployedContract.options.address,
              sourceCode: sourceCode,
            };
            console.log(data)
            const url = 'https://api-testnet.bscscan.com'
            const response = await fetch(url, {
              method: 'POST',
              headers: {
                'Content-Type': 'application/json',
              },
              body: JSON.stringify(data)
            });
            const jsonResp = await response
            console.log(jsonResp);
            return jsonResp;
      })
    }
    const resetForm = () => {
      instance.ctx.$refs['vForm'].resetFields()
    }
    return {
      ...toRefs(state),
      submitForm,
      resetForm,
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
