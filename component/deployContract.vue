<template>
  <el-form :model="formData" ref="vForm" :rules="rules" label-position="top" label-width="80px" size="default"
    @submit.prevent>
    <el-form-item label="代币名称" prop="input84916" class="required label-right-align">
      <el-input v-model="formData.input84916" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币简称" prop="input3108" class="required label-right-align">
      <el-input v-model="formData.input3108" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币精度" prop="input77472" class="required label-right-align">
      <el-input v-model="formData.input77472" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币总量" prop="input34416" class="required label-right-align">
      <el-input v-model="formData.input34416" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="选择模板" prop="select39851">
      <el-select v-model="formData.select39851" class="full-width-input">
        <el-option v-for="(item, index) in select39851Options" :key="index" :label="item.label"
          :value="item.value" :disabled="item.disabled"></el-option>
      </el-select>
    </el-form-item>
    <el-form v-if="displayForm">
      <el-form v-if="displayDivident">
        <el-form-item label="最低分红标准：用户持有代币数量超过该值, 才会进行分红, 该值创建代币后无法修改" prop="input54591"
          class="label-right-align">
          <el-input v-model="formData.input54591" type="text" clearable></el-input>
        </el-form-item>
      </el-form>
    <el-form v-if="displayDividentToken">
      <el-form-item label="分红代币" prop="select24237" class="label-right-align">
        <el-select v-model="formData.select24237" class="full-width-input" clearable>
          <el-option v-for="(item, index) in select24237Options" :key="index" :label="item.label"
            :value="item.value" :disabled="item.disabled"></el-option>
        </el-select>
        </el-form-item>
      </el-form>
    </el-form>

    <!--控制显示-->
    <el-form v-if="displayForm">
    <div class="static-content-item">
      <div>买入税率:</div>
    </div>
    <el-row>
      <el-col :span="12" class="grid-cell">
        <el-row>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="回流税率" prop="input50891" class="label-right-align">
              <el-input v-model="formData.input50891" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="营销税率" prop="input89583" class="label-right-align">
              <el-input v-model="formData.input89583" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="12" class="grid-cell">
        <el-row>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="销毁税率" prop="input77801" class="label-right-align">
              <el-input v-model="formData.input77801" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="分红税率" prop="input74986" class="label-right-align">
              <el-input v-model="formData.input74986" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
    <div class="static-content-item">
      <div>卖出税率</div>
    </div>
    <el-row>
      <el-col :span="12" class="grid-cell">
        <el-row>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="回流税率" prop="input35822" class="label-right-align">
              <el-input v-model="formData.input35822" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="营销税率" prop="input52556" class="label-right-align">
              <el-input v-model="formData.input52556" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-col>
      <el-col :span="12" class="grid-cell">
        <el-row>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="销毁税率" prop="input25672" class="label-right-align">
              <el-input v-model="formData.input25672" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12" class="grid-cell">
            <el-form-item label="分红税率" prop="input101223" class="label-right-align">
              <el-input v-model="formData.input101223" type="text" clearable></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-col>
    </el-row>

    <el-form v-if="displayFund">
      <el-form-item label="营销钱包：营销税将会自动转移到此钱包中, 请务必保存好私钥" prop="input106699" class="label-right-align">
        <el-input v-model="formData.input106699" type="text" clearable></el-input>
      </el-form-item>
    </el-form>
    <el-form-item label="选择底池：添加流动性时需要添加代币与底池代币之间的交易对, 否则无法进行正常分红与回流" prop="select72992">
      <el-select v-model="formData.select72992" class="full-width-input" clearable placeholder="请选择">
        <el-option v-for="(item, index) in select72992Options" :key="index" :label="item.label"
          :value="item.value" :disabled="item.disabled"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="选择交易所" prop="select37418" class="label-right-align">
      <el-select v-model="formData.select37418" class="full-width-input" clearable>
        <el-option v-for="(item, index) in select37418Options" :key="index" :label="item.label"
          :value="item.value" :disabled="item.disabled"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="手动开启交易：添加池子后的首次交易需要在控制台手动开启(如关闭, 则添加流动性后立即可以进行交易), 交易开启后无法关闭" prop="switch16694">
      <el-switch v-model="formData.switch16694"></el-switch>
    </el-form-item>
    <el-form-item label="杀区块：将对开启交易后在n个区块内交易的地址全部拉入黑名单, 用于防止机器人抢跑买入, 必须手动开启交易" prop="switch22379"
      class="label-right-align">
      <el-switch v-model="formData.switch22379"></el-switch>
    </el-form-item>
    <el-row v-show="formData.switch22379">
      <el-col :span="12" class="grid-cell">
        <el-form-item label="区块数量:将对开启交易后在n个区块内交易的地址全部拉入黑名单, 用于防止机器人抢跑买入, 必须手动开启交易" prop="input67697"
          class="label-right-align">
          <el-input v-model="formData.input67697" type="text" placeholder="max:10" clearable></el-input>
        </el-form-item>
      </el-col>
    </el-row>
    <el-form-item label="税率开关：可在创建代币后手动调整税率, 买卖税率各不能超过25%, 此开关关闭后无法再次开启" prop="switch19287"
      class="label-right-align">
      <el-switch v-model="formData.switch19287"></el-switch>
    </el-form-item>
    <el-form-item label="转账扣费开关：开启开关后, 用户向其他地址转移代币时, 将以卖出税作为转账税率, 关闭此开关, 则转账不扣税" prop="switch38297"
      class="label-right-align">
      <el-switch v-model="formData.switch38297"></el-switch>
    </el-form-item>
    <el-form-item label="地址裂变：开启开关后, 用户交易时, 将会自动向随机地址空投小额代币, 以增加持币地址" prop="switch77035"
      class="label-right-align">
      <el-switch v-model="formData.switch77035"></el-switch>
    </el-form-item>
    <el-form-item label="黑名单功能：可拉黑部分钱包地址令其无法交易, 此开关关闭后无法再次开启" prop="switch62669" class="label-right-align">
      <el-switch v-model="formData.switch62669"></el-switch>
    </el-form-item>
    <el-form-item label="限制交易：可设置单次交易的最大交易数量, 此开关关闭后无法再次开启" prop="switch117946" class="label-right-align">
      <el-switch v-model="formData.switch117946"></el-switch>
    </el-form-item>
    <el-row v-show="formData.switch117946">
      <el-col :span="12" class="grid-cell">
        <el-form-item label="限制买入数量" prop="input27527" class="label-right-align">
          <el-input v-model="formData.input27527" type="text" clearable></el-input>
        </el-form-item>
        <div class="static-content-item">
          <div>可设置单次交易的最大交易数量, 此开关关闭后无法再次开启</div>
        </div>
      </el-col>
      <el-col :span="12" class="grid-cell">
        <el-form-item label="限制卖出数量" prop="input67682" class="label-right-align">
          <el-input v-model="formData.input67682" type="text" clearable></el-input>
        </el-form-item>
      </el-col>
    </el-row>
    <el-form-item label="限制最大持币量：可设置单个钱包持有的最大代币数量, 此开关关闭后无法再次开启" prop="switch76742" class="label-right-align">
      <el-switch v-model="formData.switch76742"></el-switch>
    </el-form-item>
    <el-row v-show="formData.switch76742">
      <el-col :span="12" class="grid-cell">
        <el-form-item label="最大持币数量：可设置单个钱包持有的最大代币数量, 此开关关闭后无法再次开启" prop="input101367"
          class="label-right-align">
          <el-input v-model="formData.input101367" type="text" clearable></el-input>
        </el-form-item>
      </el-col>
      <el-col :span="12" class="grid-cell">
      </el-col>
    </el-row>
  </el-form>

    <div class="static-content-item">
      <el-button type="primary" @click="submitForm">创建代币</el-button>
    </div>
  </el-form>
</template>

<script>
  import {
    defineComponent,
    toRefs,
    watch,
    ref,
    reactive,
    getCurrentInstance
  }
  from 'vue'

  import {
    ethAddress,
    supportedChainIds,
    templateA_bytecode,
    TemplateA_ABI,
    templateB_bytecode,
    TemplateB_ABI,
    templateC_bytecode,
    TemplateC_ABI,
    templateD_bytecode,
    TemplateD_ABI,
  } from '@/utils/chain'
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
          select39851: 1,
          input54591: "",
          select24237: "",
          input50891: "",
          input89583: "",
          input77801: "",
          input74986: "",
          input35822: "",
          input52556: "",
          input25672: "",
          input101223: "",
          input106699: "",
          select72992: "",
          select37418: "",
          switch16694: false,
          switch22379: false,
          input67697: "",
          switch19287: false,
          switch38297: null,
          switch77035: null,
          switch62669: null,
          switch117946: false,
          input27527: "",
          input67682: "",
          switch76742: null,
          input101367: "",
        },
        rules: {
          input84916: [{
            required: true,
            message: '代币名称不能为空',
          }],
          input3108: [{
            required: true,
            message: '代币简称不能为空',
          }],
          input77472: [{
            required: true,
            message: '代币精度不能为空',
          }, {
            pattern: /^\d+(\.\d+)?$/,
            trigger: ['blur', 'change'],
            message: '精度只能为数字'
          }],
          input34416: [{
            required: true,
            message: '代币总量不能为空',
          }, {
            pattern: /^\d+(\.\d+)?$/,
            trigger: ['blur', 'change'],
            message: '总量只能为数字'
          }],
        },
        select39851Options: [{
          "label": "无税通用模板",
          "value": 1
        }, {
          "label": "有税回流模板",
          "value": 2
        }, {
          "label": "持币分红模板",
          "value": 3
        }, {
          "value": 4,
          "label": "加池分红模板"
        }],
        select24237Options: [{
          "label": "BNB",
          "value": 1
        }, {
          "label": "BUSD",
          "value": 2
        }, {
          "label": "CAKE",
          "value": 3
        }],
        select72992Options: [{
          "label": "BNB",
          "value": 1
        }, {
          "label": "USDT",
          "value": 2
        }],
        select37418Options: [{
          "label": "Pancakeswap",
          "value": 1
        }],
      })

      const displayForm = ref(false);
      const displayDivident = ref(false);
      const displayDividentToken = ref(false);
      const displayFund = ref(false);
      //监听下拉框弹出窗口
      watch(() =>state.formData.select39851, (newValue, oldValue) => {
        console.log(newValue, oldValue);
        if (newValue != oldValue && newValue == '2') {
          displayForm.value = true;
          displayDivident.value = false;
          displayDividentToken.value = false;
          displayFund.value = false;
        } else if (newValue != oldValue && newValue == '3') {
          displayForm.value = true;
          displayDivident.value = true;
          displayDividentToken.value = true;
          displayFund.value = false;
        } else if (newValue != oldValue && newValue == '4') {
          displayForm.value = true;
          displayDivident.value = false;
          displayDividentToken.value = true;
          displayFund.value = true;
        } else {
          displayForm.value = false;
          displayDivident.value = false;
          displayDividentToken.value = false;
          displayFund.value = false;
        }
      });

      const instance = getCurrentInstance()
      const submitForm = () => {
        instance.ctx.$refs['vForm'].validate(async (valid) => {
          if (!valid) return
          // token信息
          // 名称
          const name = state.formData.input84916;
          // 简称
          const symbol = state.formData.input3108;
          // 精度
          const decimal = state.formData.input77472;
          // 供应
          const supply = state.formData.input34416;
          // 模板类型
          const isTemplates = state.formData.select39851;
          // 最低分红标准
          const minDivident = state.formData.input54591;
          // 分红代币
          const dividentToken = state.formData.select24237;
          /** 买入税率 */
          // 回流税率
          const buyLpFee = state.formData.input50891;
          // 营销税率
          const buyFundFee = state.formData.input89583;
          // 销毁税率
          const buyBurnFee = state.formData.input77801;
          // 分红税率
          const buyDividentFee = state.formData.input74986;
          /** 卖出税率 */
          // 回流税率
          const sellLpFee = state.formData.input35822;
          // 营销税率
          const sellFundFee = state.formData.input52556;
          // 销毁税率
          const sellBurnFee = state.formData.input25672;
          // 分红税率
          const sellDividentFee = state.formData.input101223;      
          
          // 营销钱包
          const fundAddress = state.formData.input106699;
          // 选择底池
          const lpPool = state.formData.select72992;
          // 选择交易所
          const exchange = state.formData.select37418;
          // 手动开启交易
          const enableOffTrade = state.formData.switch16694;
          // 杀区块
          const enableKillBlock = state.formData.switch22379;
          const killBlock = state.formData.input67697;
          // 税率开关
          const enableChangeTax = state.formData.switch19287;
          // 转账扣费
          const enableTransferFee = state.formData.switch38297;
          // 地址裂变
          const fission = state.formData.switch77035;
          // 黑名单功能
          const enableRewardList = state.formData.switch62669;
          // 限制交易
          const enableSwapLimit = state.formData.switch117946;
          // 限制买入数量
          const buyTxLimit = state.formData.input27527;
          // 限制卖出数量
          const sellTxLimit = state.formData.input67682;
          // 限制最大持币量
          const enableWalletLimit = state.formData.switch76742;
          const maxWalletLimit = state.formData.input101367;

          // 当前是否是eth
          const currentIsEth = lpPool == 1 ? true:false;

          //TODO: 提交表单
          // 判断是否连接MetaMask
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
          // 初始化实例
          const web3 = window.web3;
          // 获取当前账户
          const accounts = await web3.eth.getAccounts();
          // 获取当前钱包的链ID，判断是否支持该链
          const chainId = await web3.eth.getChainId();
          console.log("chainId",chainId);
          if (!supportedChainIds.includes(chainId)) {
            throw new Error(`Metamask is connected to an unsupported network. Please switch to a supported network: ${supportedChainIds.join(', ')}.`);
          }

          if (isTemplates == 1) {
            console.log("prepare deploy", isTemplates)
            const abi = TemplateA_ABI;
            const bytecode = templateA_bytecode;
            const contract = new web3.eth.Contract(abi);
            const supplyInWei = web3.utils.toBN(supply);
            // 计算 10 的 decimals 次方，即代币的精度
            const precision = web3.utils.toBN(10).pow(web3.utils.toBN(parseInt(decimal)));

            const estimatedGas = contract.deploy({
              data: bytecode,
              arguments: [
                [name, symbol],
                [],
                [web3.utils.toBN(parseInt(decimal)), precision],
                [],
              ],
            }).estimateGas();
            const gasPrice = await web3.eth.getGasPrice();
            const finalGas = Math.floor(estimatedGas * 1.2); // 增加一个因子
            
            // 打包初始化参数
            const constructorArgs = [
                [name, symbol],
                [],
                [web3.utils.toBN(decimal), web3.utils.toWei(supply, "ether")],
                [],
            ];
            const encodedArgs = web3.eth.abi.encodeParameters(['string[]', 'address[]', 'uint256[]', 'bool[]'], constructorArgs);
            // 部署合约
            const deployedContract = await contract.deploy({
              data: bytecode,
              arguments: constructorArgs,
            }).send({
                from: accounts[0],
                gas: finalGas,
                gasPrice: gasPrice * 1.2 // 增加一个因子
            }, (error, transactionHash) => {
              if (error) {
                console.error(error);
              } else {
                console.log(transactionHash);
              }
            })

            // 在区块链浏览器中验证
            const sourceCode = await web3.eth.getCode(deployedContract.options.address);
            console.log("合约地址:",deployedContract.options.address);
            console.log("源码:",sourceCode);
            const data = {
              apikey: 'CIFMXUC696VIJ1RZ3FERDUK3YKVT88JWKP',
              module: 'contract',
              action: 'verifysourcecode',
              sourceCode: sourceCode,
              contractaddress: deployedContract.options.address,
              codeformat:'solidity-single-file',
              contractname: 'CoinLockToken',
              compilerversion: 'v0.8.4+commit.c7e474f2',
              optimizationused:1,
              runs:200,
              constructorArguements: encodedArgs,
            };
            console.log(data)
            const url = 'https://api-testnet.bscscan.com/api'
            const response = await fetch(url, {
              method: 'POST',
              headers: {
                'Content-Type': 'application/x-www-form-urlencoded',
              },
              body: JSON.stringify(data)
            });
            const resp = await response.json();
            console.log(resp.result);

            
          } else if (isTemplates == 2) {
            console.log("prepare deploy", isTemplates)
            const abi = TemplateB_ABI;
            const bytecode = templateB_bytecode;
            const contract = new web3.eth.Contract(abi);
            
            const estimatedGas = contract.deploy({
              data: bytecode,
              arguments: [
                [name, symbol],
                [],
                [web3.utils.toBN(parseInt(decimal)), precision],
                [],
              ],
            }).estimateGas();
            const gasPrice = await web3.eth.getGasPrice();
            const finalGas = Math.floor(estimatedGas * 1.2); // 增加一个因子
            
            const deployedContract = await contract.deploy({
              data: bytecode,
              arguments: [
                [name, symbol],
                [
                  ethAddress[3],
                  '0x9Ac64Cc6e4415144C455BD8E4837Fea55603e5c3',
                  accounts[0],
                  accounts[0],
                ],
                [
                  web3.utils.toBN(decimal), 
                  web3.utils.toBN(supply),
                  web3.utils.toBN(buyFundFee),
                  web3.utils.toBN(buyBurnFee),
                  web3.utils.toBN(buyLpFee),
                  web3.utils.toBN(sellFundFee),
                  web3.utils.toBN(sellBurnFee),
                  web3.utils.toBN(sellLpFee),
                  web3.utils.toBN(killBlock),
                  web3.utils.toBN(buyTxLimit),
                  web3.utils.toBN(sellTxLimit),
                  web3.utils.toBN(maxWalletLimit),
                  web3.utils.toBN(maxWalletLimit),
                ],
                [
                  currentIsEth,
                  enableOffTrade,
                  enableKillBlock,
                  enableRewardList,
                  enableSwapLimit,
                  enableWalletLimit,
                  enableChangeTax,
                  enableTransferFee,
                ],
              ],
            }).send({
                from: accounts[0],
                gas: '5000000',
                gasPrice: web3.utils.toWei('5', 'gwei'),
              }, (error, transactionHash) => {
                if (error) {
                  console.error(error);
                } else {
                  console.log(transactionHash);
                }
              })

          } else if (isTemplates == 3) {

          
          } else if (isTemplates == 4) {
            
          }
        })
      }
      return {
        ...toRefs(state),
        displayForm,
        displayDivident,
        displayDividentToken,
        displayFund,
        submitForm,
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
