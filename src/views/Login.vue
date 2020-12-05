<template>
  <a-form :label-col="labelCol" :wrapper-col="wrapperCol">
    <a-form-item label="用户名" v-bind="validateInfos.userName">
      <a-input v-model:value="data.userName" />
    </a-form-item>
    <a-form-item label="密码" v-bind="validateInfos.passWord">
      <a-input v-model:value="data.passWord" />
    </a-form-item>
    <a-form-item :wrapper-col="{ span: 14, offset: 4 }">
      <a-button type="primary" @click="onSubmit">
        登陆
      </a-button>
    </a-form-item>
  </a-form>
</template>
<script>
import { reactive, toRaw } from "vue";
import { useForm } from "@ant-design-vue/use";
import { setToken } from "../utils/auth";
export default {
  setup() {
    const data = reactive({
      userName: "",
      passWord: ""
    });
    const { validate, validateInfos } = useForm(
      data,
      reactive({
        userName: [
          {
            required: true,
            message: "请输入用户名"
          }
        ],
        passWord: [
          {
            required: true,
            message: "请输入密码"
          }
        ]
      })
    );
    const onSubmit = e => {
      e.preventDefault();
      validate()
        .then(res => {
          setToken(res.passWord);
          console.log(res, toRaw(data));
        })
        .catch(err => {
          console.log("error", err);
        });
    };
    return {
      labelCol: { span: 4 },
      wrapperCol: { span: 14 },
      validateInfos,
      data,
      onSubmit
    };
  }
};
</script>


Challenge A

 

Rewrite the following functions double, incrementand foorespectively (Do not merge them into one function!) by applying DRY principle and functional program paradigm with modern Javascript features so that it's written in a more idiomatic Javascript way.

 

If you are not familar with functional programming in Javascript, learn more here: https://blog.fundebug.com/2019/08/09/learn-javascript-functional-programming/.

评分标准
 

请使用Javascript(ES6+) 来编写代码完成以上测试题，但不能使用伪代码，提交的代码必须是可执行的代码。

 

请确保该代码充分体现了阁下对现代JavaScript 语法、特性以及编码规范的熟练掌握，以及对于代码模块化设计、代码可读性的理解。

 

我们会通过以下评分标准来评估阁下的解答，请在提交之前按照该标准检查：

  正确完整地实现了原代码的业务逻辑- 50%
  合理运用现代Javascript 的函数式编程特性- 50%
请在此上传代码文件（请将.js 后缀改为.es6）
