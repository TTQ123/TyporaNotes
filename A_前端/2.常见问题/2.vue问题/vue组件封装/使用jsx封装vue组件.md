# 1.如何在vue3中使用jsx

![image-20231116171340850](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231116171340850.png)

# 2.封装一个弹窗一个弹窗组件

jsx文件

```jsx
// 封装一个弹窗组件 用函数配置形式
// 导入createApp来挂载节点
import { createApp } from 'vue'

// 模态框样式
const divModel = {
    position: 'fixed',
    top: '0',
    left: '0',
    width: '100%',
    height: '100%',
    backgroundColor: '#00000050',
    display: 'flex',
    justifyContent: 'center',
    alignItems: 'center'
}

// 弹窗样式
const box = {
    width: '500px',
    height: '100px',
    backgroundColor: '#fff',
    padding: '20px',
    borderRadius: '8px',
    boxShadow: '0 2px 4px rgba(0, 0, 0, 0.2)',
    textAlign: 'center',
}

const text = {
    marginBottom: '20px'
}

const button = {
    padding: '8px 16px',
    backgroundColor: '#007bff',
    color: '#fff',
    border: 'none',
    borderRadius: '4px',
    cursor: 'pointer'
}

// 定义一个弹窗组件的配置对象
const MessageBox = {
    // 定义弹窗组件的 props，msg 为必传参数，类型为字符串
    props: {
        msg: {
            type: String,
            required: true
        }
    },
    // 定义弹窗组件的渲染函数
    render(ctx) {
        // 获取组件的 props 和 emit 方法
        const { $props, $emit } = ctx
        // 返回弹窗组件的 JSX
        return (
            <div style={divModel}>
                <div class="box" style={box} >
                    <div class="text" style={text}>{$props.msg}</div>
                    <button click={$emit('onClick')} style={button}>关闭</button>
                </div>
            </div>
        );
    }
}

export function showMsg(msg, onClick) {
    // 创建一个div并添加到body上
    const div = document.createElement('div');
    document.body.appendChild(div);
    // 渲染弹窗组件到页面上
    const app = createApp(MessageBox, {
        msg,
        // 点击按钮时触发onClick事件
        onClick() {
            // 调用 onClick 回调函数，并在回调函数执行完毕后卸载组件并移除 div
            onClick(() => {
                app.unmount()
                div.remove()
            })
        }
    })
    // 挂载节点
    app.mount(div)
}
```

vue

```vue
<template>
    <div>
        <button @click="openMsgBox">显示弹窗</button>
    </div>
</template>

<script setup>
import { showMsg } from '@/uitls/showMsg.jsx'
const openMsgBox = () => {
    // 点击时调用showMsg 传递参数msg 还有 一个关闭的方法
    showMsg('显示弹窗', (onClick) => { onClick() })
}
</script>
```

