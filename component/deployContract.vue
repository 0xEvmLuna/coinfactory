<template>
  <el-form :model="formData" ref="vForm" :rules="rules" label-position="top" label-width="80px" size="default"
    @submit.prevent>
    <el-form-item label="代币名称" prop="input84916" class="label-right-align">
      <el-input v-model="formData.input84916" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币简称" prop="input3108" class="label-right-align">
      <el-input v-model="formData.input3108" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币精度" prop="input77472" class="label-right-align">
      <el-input v-model="formData.input77472" type="text" clearable></el-input>
    </el-form-item>
    <el-form-item label="代币总量" prop="input34416" class="label-right-align">
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
      <el-form-item label="限制最大持币量：可设置单个钱包持有的最大代币数量, 此开关关闭后无法再次开启" prop="switch76742" class="label-right-align">
        <el-switch v-model="formData.switch76742"></el-switch>
      </el-form-item>
    </el-form>

          <div class="static-content-item">
        <el-button type="primary">创建代币</el-button>
      </div>
  </el-form>
</template>

<script>
  import {
    defineComponent,
    ref,
    toRefs,
    watch,
    reactive,
    getCurrentInstance
  }
  from 'vue'
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
          switch19287: false,
          switch38297: null,
          switch77035: null,
          switch62669: null,
          switch117946: null,
          switch76742: null,
        },
        rules: {},
        select39851Options: [{
          "label": "无税通用模板",
          "value": 1
        }, {
          "label": "有税通用模板",
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
        instance.ctx.$refs['vForm'].validate(valid => {
          if (!valid) return
          //TODO: 提交表单
        })
      }
      const resetForm = () => {
        instance.ctx.$refs['vForm'].resetFields()
      }
      return {
        ...toRefs(state),
        displayForm,
        displayDivident,
        displayDividentToken,
        displayFund,
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
