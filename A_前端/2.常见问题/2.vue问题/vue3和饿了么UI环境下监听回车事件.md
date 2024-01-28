参考了文章

https://blog.csdn.net/m0_63732435/article/details/134183461

不过这片文章时vue2的写法



**在Vue3中，直接注册监听回车事件是没有用的，要在生命周期钩子函数中监听事件和销毁事件才可以生效**



项目实际应用

由于本项目注册和登录是写在同一个页面的,所以涉及了登录和注册同时写

![image-20231119225057993](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119225057993.png)

给登录按钮绑定

![image-20231119225114249](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119225114249.png)

给注册按钮绑定

![image-20231119225125662](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231119225125662.png)



完整代码

```vue
<!-- 登录页注册页 -->
<script setup>
import { userRegisterService, userLoginService } from '@/api/user.js'
import { User, Lock } from '@element-plus/icons-vue'
import { onMounted, ref, watch, onBeforeUnmount } from 'vue'
import { useUserStore } from '@/stores'
import { useRouter } from 'vue-router'

const isRegister = ref(true)
// ref对象 绑定表单组件
const form = ref()
// 提交注册的表单对象
const formModel = ref({
  username: '',
  password: '',
  repassword: ''
})
// 整个表单的校验规则
const rules = {
  // 表单校验规则（要根据接口文档来具体书写）
  // 1.非空校验 required  message 消息提示 trigger 校验时机
  // 2.长度校验 min:xxx,max:xxx
  // 3.正则校验 pattern：正则规则
  // 4.支持自定义校验 => 自己写校验函数
  username: [
    { required: true, message: '请输入用户名', trigger: 'blur' },
    {
      min: 5,
      max: 10,
      message: '用户名必须是5-10位的数字字母',
      trigger: 'blur'
    }
  ],
  password: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    {
      pattern: /^\S{6,15}$/,
      message: '密码必须是6-15位的非空字符',
      trigger: 'blur'
    }
  ],
  repassword: [
    { required: true, message: '请输入密码', trigger: 'blur' },
    {
      pattern: /^\S{6,15}$/,
      message: '密码必须是6-15位的非空字符',
      trigger: 'blur'
    },
    {
      // 校验函数
      validator: (rule, value, callback) => {
        // 校验俩次的密码是否一直
        if (value !== formModel.value.password) {
          callback(new Error('俩次输入的密码不一致'))
        } else {
          callback() //就算成功也要callback
        }
      },
      trigger: 'blur'
    }
  ]
}

// 注册预校验
const register = async () => {
  // 注册成功之前先进行预校验,校验成功发起注册请求 -> 校验失败会自动提示我们只要处理校验成功的
  // 找到表单对象 调用它的方法会返回一个promise对象(判断校验是否成功,所以要等待)
  await form.value.validate()
  // 如果前面失败了不会走到这里  发起请求
  await userRegisterService(formModel.value)
  ElMessage.success('注册成功')
  // 切换到登录(这里也可以做成一个路由 但是比较麻烦)
  isRegister.value = true
}

// 登录预校验
const userStore = useUserStore()

// 路由操作用router
// 路由信息用route
const router = useRouter()
const login = async () => {
  await form.value.validate()
  const res = await userLoginService(formModel.value)
  // 将请求到token存到pinia中
  userStore.setToken(res.data.token)
  ElMessage.success('登录成功')
  router.push('/')
}

// 切换时清空表单内容(利用watch来监视ref变量就是在监视切换)
watch(isRegister, () => {
  formModel.value = {
    username: '',
    password: '',
    repassword: ''
  }
})

// 回车时也会触发登录或者注册
const keyDown = (e) => {
  if (e.keyCode === 13 && isRegister.value === true) {
    login()
  } else if (e.keyCode === 13 && isRegister.value === false) {
    register()
  }
}

// 在组件加载时开始监听事件
onMounted(() => {
  // 绑定监听事件
  window.addEventListener('keydown', keyDown)
})

// 在组件卸载时开始销毁监听事件
onBeforeUnmount(() => {
  // 销毁事件
  window.removeEventListener('keydown', keyDown, false)
})
</script>

<template>
  <el-row class="login-page">
    <el-col :span="12" class="bg"></el-col>
    <el-col :span="6" :offset="3" class="form">
      <el-form
        :model="formModel"
        :rules="rules"
        ref="form"
        size="large"
        autocomplete="off"
        v-if="isRegister"
      >
        <el-form-item>
          <h1>登录</h1>
        </el-form-item>
        <el-form-item prop="username">
          <el-input
            v-model="formModel.username"
            :prefix-icon="User"
            placeholder="请输入用户名"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            v-model="formModel.password"
            name="password"
            :prefix-icon="Lock"
            type="password"
            placeholder="请输入密码"
          ></el-input>
        </el-form-item>
        <el-form-item class="flex">
          <div class="flex">
            <el-checkbox>记住我</el-checkbox>
            <el-link type="primary" :underline="false">忘记密码？</el-link>
          </div>
        </el-form-item>
        <el-form-item>
          <el-button
            @click="login"
            class="button"
            type="primary"
            auto-insert-space
            @keyup.enter="keyDown(e)"
            >登录</el-button
          >
        </el-form-item>
        <el-form-item class="flex">
          <el-link type="info" :underline="false" @click="isRegister = false">
            注册 →
          </el-link>
        </el-form-item>
      </el-form>
      <el-form
        :model="formModel"
        :rules="rules"
        ref="form"
        size="large"
        autocomplete="off"
        v-else
      >
        <el-form-item>
          <h1>注册</h1>
        </el-form-item>
        <el-form-item prop="username">
          <el-input
            v-model="formModel.username"
            :prefix-icon="User"
            placeholder="请输入用户名"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            v-model="formModel.password"
            :prefix-icon="Lock"
            type="password"
            placeholder="请输入密码"
            show-password
          ></el-input>
        </el-form-item>
        <el-form-item prop="repassword">
          <el-input
            v-model="formModel.repassword"
            :prefix-icon="Lock"
            type="password"
            placeholder="请输入再次密码"
            show-password
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button
            @click="register"
            class="button"
            type="primary"
            auto-insert-space
            @keyup.enter="keyDown(e)"
          >
            注册
          </el-button>
        </el-form-item>
        <el-form-item class="flex">
          <el-link type="info" :underline="false" @click="isRegister = true">
            ← 返回
          </el-link>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>

<style lang="scss" scoped>
.login-page {
  height: 100vh;
  background-color: #fff;

  // // 进入动画和离开动画的生效状态
  // .fade-enter-active,
  // .fade-leave-active {
  //   transition: opacity 0.25s linear;
  // }

  // // 进入动画的起始状态
  // .fade-enter-from {
  //   opacity: 0;
  //   transform: translateX(60px);
  // }
  // // 离开动画的结束状态
  // .fade-leave-to {
  //   opacity: 0;
  //   transform: translateX(60px);
  // }
  .bg {
    background:
    // 设置了俩个图片 第一个图片是logo 黑色背景的logo 放在居中的位置
    // 240px auto：这是图片的宽度和高度设置，240px表示图片宽度为240像素
    // auto表示图片高度会自动调整以保持原始图片的纵横比例。
      url('@/assets/logo2.png') no-repeat 60% center / 240px auto,
      url('@/assets/login_bg.jpg') no-repeat center / cover;
    border-radius: 0 20px 20px 0;
  }
  // form 表示右边的那六份 把这一整个设为弹性盒子
  .form {
    // 设置成一倍缩放
    transform: scale(1);
    display: flex;
    // 主轴方向设为垂直
    // 主轴居中就是在屏幕中间  因为整个屏幕已经分为左右(右边12份 form占6份) 右边3:6:3 占据一半
    flex-direction: column;
    // 定义子元素在主轴方向的对齐(此时变成了垂直方向)
    justify-content: center;
    // 无法选中某个按钮的文本或某个图像
    user-select: none;
    .title {
      margin: 0 auto;
    }
    .button {
      width: 100%;
    }
    .flex {
      // 让这个表单项靠俩测居中
      width: 100%;
      display: flex;
      justify-content: space-between;
    }
  }
}
</style>
```

