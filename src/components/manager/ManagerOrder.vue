<script setup>
import Mock from '../../mock/Mock'
import Tools from '../../tools/Tools'
import { ref, onMounted } from 'vue'
import { ElMessage } from 'element-plus'

const queryParams = ref({
    state:"",
    user:"",
    name:"",
    sendTime:"",
    payTime:""
})
const orderList = ref([])

onMounted(() => {
    orderList.value = Mock.getManagerOrder();
})

function search() {
    ElMessage({
        type:'success',
        message:'请求参数：' + JSON.stringify(queryParams.value)
    })
    orderList.value = Mock.getManagerOrder();
}
function clear() {
    queryParams.value = {
        state:"",
        user:"",
        name:"",
        sendTime:"",
        payTime:""
    }
    managerList.value = Mock.getManagerOrder();
}
function exportData() {
    Tools.exportJson('店长订单.json', JSON.stringify(orderList.value));
}
</script>
<template>
    <div class="content-container" direction="vertical">
        <div>
            <el-container class="content-row">
                <div class="input-tip">
                    订单状态:
                </div>
                <div class="input-field">
                    <el-input v-model="queryParams.state"></el-input>
                </div>
                <div class="input-tip">
                    订单名称:
                </div>
                <div class="input-field">
                    <el-input v-model="queryParams.name"></el-input>
                </div>
                <div class="input-tip">
                    用户名称:
                </div>
                <div class="input-field">
                    <el-input v-model="queryParams.user"></el-input>
                </div>
            </el-container>
            <el-container class="content-row">
                <div class="input-tip">
                    发货时间:
                </div>
                <div class="input-field">
                    <el-date-picker
                    type="daterange"
                    range-separator="至"
                    start-placeholder="开始日期"
                    end-placeholder="结束日期"
                    v-model="queryParams.sendTime">
                    </el-date-picker>
                </div>    
                <div class="input-tip">
                    支付时间:
                </div>
                <div class="input-field">
                    <el-date-picker
                    type="daterange"
                    range-separator="至"
                    start-placeholder="开始日期"
                    end-placeholder="结束日期"
                    v-model="queryParams.payTime">
                    </el-date-picker>
                </div>  
            </el-container>
            <el-container class="content-row">
                <el-button type="primary" @click="search">搜索</el-button>
                <el-button type="primary" @click="clear">清空搜索条件</el-button>
                <el-button type="primary" @click="exportData">导出</el-button>
            </el-container>
        </div>
        <div>
            <el-table
            :data="orderList"
            tooltip-effect="dark"
            style="width: 100%">
                <el-table-column
                label="类型"
                width="100"
                prop="state">
                </el-table-column>
                <el-table-column
                label="名称"
                width="300"
                prop="name">
                </el-table-column>
                <el-table-column
                label="订单号"
                width="200"
                prop="id">
                </el-table-column>
                <el-table-column
                label="店长信息"
                width="200"
                prop="manager">
                </el-table-column>
                <el-table-column
                label="件数"
                width="100"
                prop="count"
                >
                </el-table-column>
                <el-table-column
                label="价格"
                width="100"
                prop="price">            
                </el-table-column>
                <el-table-column
                label="佣金"
                width="100"
                prop="coin"> 
                </el-table-column>
                <el-table-column
                label="支付时间"
                width="200"
                prop="payTime">
                </el-table-column>
                <el-table-column
                label="发货时间"
                width="200"
                prop="sendTime">
                </el-table-column>
            </el-table>
        </div>
    </div>
</template>
