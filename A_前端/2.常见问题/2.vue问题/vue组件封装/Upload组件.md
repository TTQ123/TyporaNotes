1.upload组件

```vue
<template>
<!-- 封装图片上传组件 -->
    <el-upload
        class="avatar-uploader"
        action="https://jsonplaceholder.typicode.com/posts/"
        :show-file-list="false"
        :auto-upload="false"
        :on-change="handleChange"
    >
        <img
            v-if="props.avatar"
            :src="uploadAvatar"
            class="avatar"
        />
        <el-icon
            v-else
            class="avatar-uploader-icon"
        >
            <Plus />
        </el-icon>
    </el-upload>
</template>

<script setup>
import { Plus } from "@element-plus/icons-vue";
import {computed} from 'vue'
//每次选择完图片之后的回调

const props = defineProps({
    avatar:String
})

const emit = defineEmits(["kerwinchange"])

const uploadAvatar = computed(
  () =>
    props.avatar.includes("blob")
      ? props.avatar
      : "http://localhost:3000" + props.avatar
);


const handleChange = file => {
    emit("imgUrlChange",file.raw)
};
</script>

<style lang="scss" scoped>

::v-deep .el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  transition: var(--el-transition-duration-fast);
}

::v-deep .el-upload:hover {
  border-color: var(--el-color-primary);
}

::v-deep .el-icon.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  text-align: center;
}
.avatar {
  width: 178px;
  height: 178px;
}
</style>
```

2.使用

```vue
<script setup>
import { ref, reactive, computed } from "vue";
import { useStore } from "vuex";
import { ElMessage } from "element-plus";
import upload from "@/utils/upload";
import Upload from '@/components/upload/Upload.vue'
// import { Upload } from "@element-plus/icons-vue/dist/types";
const store = useStore();
const { username, gender, introduction, avatar } = store.state.userInfo;
const avatarUrl = computed(
  () =>
    store.state.userInfo.avatar
      ? "http://localhost:3000" + store.state.userInfo.avatar
      : `https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png`
);

const userFormRef = ref(null);
// 回显直接拿的vuex的数据
const userForm = reactive({
  username,
  gender,
  introduction,
  avatar,
  file: null,
});
const userRules = reactive({
  username: [{ required: true, message: "请输入用户名", trigger: "blur" }],
  gender: [{ required: true, message: "请选择性别", trigger: "blur" }],
  introduction: [
    { required: true, message: "请输入用户简介", trigger: "blur" },
  ],
  avatar: [{ required: true, message: "请上传头像", trigger: "blur" }],
});

const options = [
  {
    value: 0,
    label: "保密",
  },
  {
    value: 1,
    label: "男",
  },
  {
    value: 2,
    label: "女",
  },
];

// 选择图片的回调
//每次选择完图片之后的回调
const handleChange = (file) => {
  userForm.avatar = URL.createObjectURL(file);
  userForm.file = file;
};

const submitForm = () => {
  // 表单提交后会进行校验
  userFormRef.value.validate(async (valid) => {
    if (valid) {
      const res = await upload("/adminapi/user/upload", userForm);
      if (res.ActionType === "OK") {
        store.commit("changeUserInfo", res.data);
        ElMessage.success("更新成功");
      }
    }
  });
};
</script>

<template>
  <div>
    <el-page-header :icon="null" title="企业门户后台管理系统">
      <template #content>
        <span class="text-large font-600 mr-3"> 个人中心 </span>
      </template>
    </el-page-header>

    <el-row :gutter="20" style="margin-top: 20px">
      <el-col :span="8">
        <el-card>
          <div class="user-img">
            <el-image
              style="width: 120px; height: 120px"
              :src="avatarUrl"
              :zoom-rate="1.2"
              :max-scale="7"
              :min-scale="0.2"
              :preview-src-list="[avatarUrl]"
              fit="cover"
            />
            <div style="margin-top: 10px">
              <div style="text-algin: center; font-weight: bold">
                {{ store.state.userInfo.username }}
              </div>
              <div style="text-algin: center">
                {{ store.state.userInfo.role === 1 ? "管理员" : "编辑" }}
              </div>
            </div>
          </div>
        </el-card>
      </el-col>

      <el-col :span="16">
        <el-card>
          <el-form
            ref="userFormRef"
            :model="userForm"
            :rules="userRules"
            label-width="auto"
            class="demo-ruleForm"
          >
            <el-form-item label="用户名" prop="username">
              <el-input
                v-model="userForm.username"
                placeholder="请输入用户名"
                clearable
              />
            </el-form-item>
            <el-form-item label="性别" prop="username">
              <el-select
                v-model="userForm.gender"
                clearable
                placeholder="请选择性别"
                style="width: 100%"
              >
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
            <el-form-item label="简介" prop="introduction">
              <el-input
                v-model="userForm.introduction"
                placeholder="请输入用户简介"
                type="textarea"
                :rows="3"
                clearable
              />
            </el-form-item>
            <el-form-item label="头像" prop="avatar">
              <Upload :avatar="userForm.avatar" @imgUrlChange="handleChange" />
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submitForm">提交</el-button>
            </el-form-item>
          </el-form>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<style lang="scss" scoped>
.user-img {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
```

