```
79961
```

邮箱：

```
lux@hopesen.com.cn
```

```
Lx1010#1
```

开心树洞的路径：h5/happyBaby/#/dialogUe

git config --global user.email lux@hopesen.com.cn
email "1548429568@qq.com"
电子邮件“1548429568 @qq.com”

```
desc：图表开发（二）
1.完成了预警人数图表的初步设计，还差后端数据结构
committer： 陆兴
taskID:7678
todo:
1.虚有其表，还差功能逻辑
link: 
```

```
committer： 陆兴
desc：
1.完成心理辅导报告审核页面的流程优化
todo:
在产品原型中未给出的情况：

1.当预览报告后再返回到报告审核页面，状态应该是怎么样未确定
2.下载的报告应该是预览时的报告，还是系统报告？
taskID:7367
link: http://192.168.1.150/zentao/task-view-7637.html?tid=esb8fy92
```

```
committer： 陆兴
desc：
1.AI开心树洞 - 文字输出形式修改 / 前端
文字输出形式修改为逐字弹出，至全部文字输出完整
taskID: 7676
todo:
1.潜在需求：应该先显示黑色框，然后出现个加载的图标，然后再逐个文字显示
2.可优化的点，可以把这个逐行显示的写成指令的形式，或者写成npm包，或者把typed.js包装起来，能够在ts中使用
link: http://192.168.1.150/zentao/task-view-7676.html?tid=esb8fy92
```

```js
SET PATH=D:\Program Files\nodejs;%PATH%
```

```
committer： 陆兴
desc：
1.修改心里预约相关字段
taskID:7665
todo:
无
link: 
```

```
committer： 陆兴
desc：图表绘制（一）
1.初步绘制出两张图表
taskID:
todo:
待和后端数据进行结合
link: 
```

```
<template>
  <div>
    <el-row :gutter="15">
      <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px">
        <el-col :span="13">
          <el-form-item label="" prop="evalCount">
            <el-select v-model="formData.evalCount" placeholder="请选择" filterable clearable
              :style="{width: '100%'}"></el-select>
          </el-form-item>
        </el-col>
        <el-col :span="24">
          <el-form-item size="large">
            <el-button type="primary" @click="submitForm">提交</el-button>
            <el-button @click="resetForm">重置</el-button>
          </el-form-item>
        </el-col>
      </el-form>
    </el-row>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      formData: {
        evalCount: '测评标题',
      },
      rules: {
        evalCount: [{
          required: true,
          message: '请选择',
          trigger: 'change'
        }],
      },
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    submitForm() {
      this.$refs['elForm'].validate(valid => {
        if (!valid) return
        // TODO 提交表单
      })
    },
    resetForm() {
      this.$refs['elForm'].resetFields()
    },
  }
}

</script>
<style>
</style>

```

