<template>
  <div class="survey-container">
    <el-form :model="surveyForm" :rules="rules" ref="surveyForm" label-width="120px">

      <el-form-item label="姓名：" prop="name">
        <el-input v-model="surveyForm.name" placeholder="请输入您的姓名" clearable style="width: 300px;"></el-input>
      </el-form-item>


      <el-form-item label="性别：" prop="gender">
        <el-radio-group v-model="surveyForm.gender">
          <el-radio label="male">男</el-radio>
          <el-radio label="female">女</el-radio>
        </el-radio-group>
      </el-form-item>


      <el-form-item label="年龄：" prop="age">
        <el-select v-model="surveyForm.age" placeholder="请选择年龄区间" style="width: 300px;">
          <el-option v-for="item in ageOptions" :key="item.value" :label="item.label" :value="item.value"></el-option>
        </el-select>
      </el-form-item>


      <el-form-item label="喜爱武器：" prop="weapon">
        <el-checkbox-group v-model="surveyForm.weapon">
          <el-checkbox v-for="(weapon, index) in weaponOptions" :key="index" :label="weapon"></el-checkbox>
        </el-checkbox-group>
      </el-form-item>


      <el-form-item>
        <el-button type="primary" @click="submitForm">
          提交问卷
        </el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      surveyForm: {
        name: '',
        gender: '',
        age: '',
        weapon: []
      },
      ageOptions: [
        { value: 'under18', label: '18岁以下' },
        { value: '18-25', label: '18-25岁' },
        { value: '25-35', label: '25-35岁' },
        { value: 'over35', label: '35岁以上' }
      ],
      weaponOptions: ['太刀', '大剑', '铳枪', '片手剑'],
      rules: {
        name: [
          { required: true, message: '请输入姓名', trigger: 'blur' }
        ],
        gender: [
          { required: true, message: '请选择性别', trigger: 'change' }
        ],
        age: [
          { required: true, message: '请选择年龄区间', trigger: 'change' }
        ],
        weapon: [
          {
            type: 'array',
            required: true,
            message: '请至少选择一个武器',
            trigger: 'change'
          }
        ]
      }
    }
  },
  methods: {
    submitForm() {
      this.$refs.surveyForm.validate((valid) => {
        if (valid) {
          this.$message.success('提交成功！')
          console.log('表单数据：', this.surveyForm)
        } else {
          this.$message.error('请完善表单内容')
          return false
        }
      })
    }
  }
}
</script>

<style scoped>
.survey-container {
  max-width: 800px;
  margin: 50px auto;
  padding: 20px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, .1);
  border-radius: 4px;
}

.el-checkbox {
  margin-right: 20px;
}
</style>