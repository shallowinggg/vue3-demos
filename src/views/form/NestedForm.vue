<template>
  <el-form :model="region" label-width="auto" ref="formRef" :rules="rules">
    <el-form-item label="名称" prop="name" :inline-message="true">
      <el-input v-model="region.name" />
    </el-form-item>
  </el-form>
</template>

<script setup>
import { defineProps, toRefs, ref } from 'vue'

const props = defineProps({
  region: {
    name: String
  }
})

const { region } = toRefs(props)

const formRef = ref()
const rules = {
  name: [{ required: true, message: '请输入地区名称', trigger: 'blur' }]
}
</script>
