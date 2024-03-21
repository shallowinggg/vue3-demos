<template>
  <el-form :model="form" ref="formRef" :rules="rules" label-width="auto">
    <el-form-item label="名称" prop="name">
      <el-input v-model="form.name" />
    </el-form-item>
    <div>
      <span>地区</span>
      <NestedForm
        v-for="(region, index) in form.regions"
        :key="index"
        :region="form.regions[index]"
        ref="regionFormRefs"
      />
    </div>
    <el-button type="primary" @click="validateForm"> Check </el-button>
  </el-form>
</template>

<script setup>
import { reactive, ref } from 'vue'
import NestedForm from './NestedForm.vue'
import { ElMessage } from 'element-plus'

// 嵌套表单校验demo
//

const form = reactive({
  name: '',
  regions: [{ name: 'region1' }, { name: 'region2' }]
})
const rules = {
  name: [{ required: true, message: '请输入名称', trigger: 'blur' }],
  regions: [{ required: true, message: '请输入地区', trigger: 'blur' }]
}
const formRef = ref()
const regionFormRefs = ref([])

const validateForm = async () => {
  const valid = await formRef.value.validate((valid, fields) => {})
  if (!valid) {
    ElMessage.error('请检查表单')
    return
  }

  for (const ref of regionFormRefs.value) {
    const form = ref.$refs.formRef
    form.validate((valid) => {
      if (!valid) {
        ElMessage.error('请检查地区表单')
        return
      }
    })
  }
  return
}
</script>
