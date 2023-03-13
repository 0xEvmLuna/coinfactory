<template>
  <div>
    <el-table :data="list">
      <el-table-column label="合约地址" prop="address">
        <template #default="{ row }">
          <div class="flex items-center">
            <span>{{ row.address }}</span>
            <el-button type="text" icon="el-icon-copy-document" @click="copyAddress(row.address)">
              复制
            </el-button>
          </div>
        </template>
      </el-table-column>
      <el-table-column label="名称" prop="name"></el-table-column>
      <el-table-column label="简称" prop="shortName"></el-table-column>
      <el-table-column label="模板" prop="template"></el-table-column>
      <el-table-column label="所有者" prop="owner">
        <template #default="{ row }">
          <div class="flex items-center">
            <span>{{ row.owner }}</span>
            <el-button type="text" icon="el-icon-copy-document" @click="copyAddress(row.owner)">
              复制
            </el-button>
          </div>
        </template>
      </el-table-column>
      <el-table-column label="创建时间" prop="createTime"></el-table-column>
      <el-table-column label="操作">
        <template #default="{ row }">
          <el-button type="primary" @click="gotoConsole(row)" class="text-blue-500">
            进入控制台
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import useClipboard from "vue-clipboard3";
//import { useRouter } from 'vue-router'
import Web3 from 'web3'

export default {
  setup() {
    const list = ref([
      {
        address: '0x1234567890abcdef',
        name: 'Contract A',
        shortName: 'A',
        template: 'Template A',
        owner: '0xabcdef1234567890',
        createTime: '2022-01-01',
      },
      {
        address: '0xfedcba0987654321',
        name: 'Contract B',
        shortName: 'B',
        template: 'Template B',
        owner: '0x90abcdef12345678',
        createTime: '2022-02-01',
      },
      {
        address: '0x13579bdf02468ace',
        name: 'Contract C',
        shortName: 'C',
        template: 'Template C',
        owner: '0x7890abcdef123456',
        createTime: '2022-03-01',
      },
      {
        address: '0x2468ace13579bdf0',
        name: 'Contract D',
        shortName: 'D',
        template: 'Template D',
        owner: '0x567890abcdef1234',
        createTime: '2022-04-01',
      },
    ]);
    //const { toClipboard } = useClipboard();

    function copyAddress(address) {
      // 复制地址到剪贴板
      const text = `${row.address}`;
      toClipboard(text);
    }

    //const router = useRouter()
    function gotoConsole(row) {
      // 进入控制台
      //router.push(`/detail/${id}`)
    }

    // 存放合约数据
    const userContracts = ref([]);


    // 在页面渲染之前执行的回调函数
    onBeforeMount(async () => {
      // 初始化实例
      const web3 = new Web3('https://data-seed-prebsc-1-s1.binance.org:8545');
      
      // 请求MetaMask授权
      const accounts = await ethereum.request({ method: "eth_requestAccounts" });
      const userAddress = accounts[0];
      const filter = {
        fromBlock: 'earliest',
        toBlock: 'latest',
        address: null,
        topics: [
          web3.utils.sha3('ContractDeployed(address)'),
          null,
          web3.utils.padLeft(userAddress, 64)
        ]
      };

      web3.eth.getPastLogs(filter)
        .then(logs => {
          const contractAddresses = logs.map(log => log.address);
          console.log(contractAddresses);
        })
        .catch(err => console.error(err));
    });

    return {
      userContracts,
      list,
      copyAddress,
      gotoConsole,
    };
  },
};
</script>
