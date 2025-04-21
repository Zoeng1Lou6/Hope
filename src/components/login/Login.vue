<template>
    <transition name="fade">
        <div id="container">
            <div id="title">
                <h1>电商后台管理系统</h1>
            </div>
            <div class="input">
                <el-input v-model="name" prefix-icon="User" placeholder="请输入用户名"></el-input>
            </div>
            <div class="input">
                <el-input v-model="password" prefix-icon="Lock" placeholder="请输入密码" auto-complete="new-password" show-password></el-input>
            </div>
            <div class="input">
                <el-button @click="login" style="width: 500px" type="primary" :disabled="disabled">登录</el-button>
            </div>
        </div>
    </transition>
</template>

<script setup>
import Storage from '../../tools/Storage'
import { ElMessage } from 'element-plus'
import { ref, computed } from 'vue'
import { useRouter } from 'vue-router'

const store = Storage()
const router = useRouter()


const name = ref("")
const password = ref("")

const disabled = computed(() => {
    return name.value.length === 0 || password.value.length === 0
})

const namePattern = /^[a-zA-Z0-9]{3,20}$/ 
const passwordPattern = /^[a-zA-Z0-9]{6,20}$/ 

function login() {
    if (!namePattern.test(name.value)) {
        ElMessage({
            message: '用户名格式不正确',
            type: 'error',
            duration: 3000
        })
        return
    }
    if (!passwordPattern.test(password.value)) {
        ElMessage({
            message: '密码格式不正确',
            type: 'error',
            duration: 3000
        })
        return
    }
    store.registUserInfo(name.value, password.value)
    ElMessage({
        message: '登录成功',
        type:'success',
        duration: 3000
    })
    setTimeout(() => {
        router.push({ name: "home" })
    }, 3000)
}
</script>

<style scoped>
#container {
    background: linear-gradient(to bottom right, #007BFF, #00BFFF);
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
}

#title {
    text-align: center;
    color: white;
    margin-top: 200px;
}

.input {
    margin: 20px auto;
    width: 500px;
}

.el-input {
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border: 2px solid transparent; 
    transition: all 0.3s ease; 
}

.el-input:hover {
    border-color: #ffffff; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); 
}

.el-input:focus-within {
    border-color: #0056b3; 
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3); 
}

.el-button {
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    transition: background-color 0.3s ease;
}

.el-button:hover {
    background-color: #0056b3;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>    
