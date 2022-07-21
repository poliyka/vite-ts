<template>
  <NGrid x-gap="12" :cols="2">
    <NGi>
      <NForm>
        <NFormItem label="身高(cm)" :validationStatus="inputHeightValidationStatus">
          <NInputNumber v-model:value="height" placeholder="請輸入身高" />
          <template #feedback>
            {{ inputHeightFeedback }}
          </template>
        </NFormItem>
        <NFormItem label="體重(Kg)" :validationStatus="inputWeightValidationStatus">
          <NInputNumber v-model:value="weight" placeholder="請輸入體重" />
          <template #feedback>
            {{ inputWeightFeedback }}
          </template>
        </NFormItem>
        <NFormItem>
          <NButton type="error" :disabled="clearBtnStatus" @click="clearBtnOnClick"> 清除 </NButton>
        </NFormItem>
      </NForm>
    </NGi>
    <NGi>
      <div class="NCenter">
        <NAlert
          :title="`Info: BMI=${bmi}`"
          type="info"
          v-if="BMIStatus == 'Normal'"
          style="width: 100%"
        >
          BMI 在正常值範圍
        </NAlert>
        <NAlert
          :title="`Danger: BMI=${bmi}`"
          type="error"
          v-else-if="BMIStatus == 'Low'"
          style="width: 100%"
        >
          體重過輕
        </NAlert>
        <NAlert
          :title="`Warning: BMI=${bmi}`"
          type="warning"
          v-else-if="BMIStatus == 'highWeight'"
          style="width: 100%"
        >
          體重過重
        </NAlert>
        <NAlert
          :title="`Warning: BMI=${bmi}`"
          type="warning"
          v-else-if="BMIStatus == 'LHighWeight'"
          style="width: 100%"
        >
          輕度肥胖
        </NAlert>
        <NAlert
          :title="`Warning: BMI=${bmi}`"
          type="warning"
          v-else-if="BMIStatus == 'MHighWeight'"
          style="width: 100%"
        >
          中度肥胖
        </NAlert>
        <NAlert
          :title="`Danger: BMI=${bmi}`"
          type="error"
          v-else-if="BMIStatus == 'OHighWeight'"
          style="width: 100%"
        >
          肥死了
        </NAlert>
      </div>
    </NGi>
  </NGrid>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import type { Ref } from "vue";
import { NForm, NInputNumber, NFormItem, NGrid, NGi, NAlert, NButton } from "naive-ui";

/****************
 * define value *
 ****************/
const height = ref<null | number>(null);
const weight = ref<null | number>(null);
const bmi = ref<number>(NaN);

// create utils function
function createValidStatus(value: number | null): undefined | "warning" | "error" {
  if (value == null) return "warning";
  if (value < 0 || value > 300) return "error";
  return undefined;
}
function createHeightFeedback(value: number | null): string {
  if (value == null) return "請輸入身高";
  if (value < 0 || value > 300) return "請輸入正常範圍";
  return "";
}
function createWeightFeedback(value: number | null): string {
  if (value == null) return "請輸入體重";
  if (value < 0 || value > 300) return "請輸入正常範圍";
  return "";
}

function createBMIStatus(
  height: number | null,
  weight: number | null,
  bmi: Ref<number>
): undefined | "Normal" | "Low" | "highWeight" | "LHighWeight" | "MHighWeight" | "OHighWeight" {
  if (height == null || weight == null) return undefined;
  if (height <= 0 || weight <= 0 || height > 300 || weight > 300) return undefined;
  bmi.value = Math.round((weight / Math.pow(height / 100, 2)) * 100) / 100;

  // check BMI
  if (isNaN(bmi.value)) return undefined;
  if (bmi.value < 18.5) return "Low";
  if (bmi.value >= 24 && bmi.value < 27) return "highWeight";
  if (bmi.value >= 27 && bmi.value < 30) return "LHighWeight";
  if (bmi.value >= 30 && bmi.value < 35) return "MHighWeight";
  if (bmi.value >= 35) return "OHighWeight";
  return "Normal";
}
function createClearBtnStatus(height: number | null, weight: number | null): boolean {
  if (height == null || weight == null) return true;
  return false;
}

// feedback
const inputHeightValidationStatus = computed(() => {
  return createValidStatus(height.value);
});
const inputWeightValidationStatus = computed(() => {
  return createValidStatus(weight.value);
});
const BMIStatus = computed(() => {
  return createBMIStatus(height.value, weight.value, bmi);
});
const clearBtnStatus = computed(() => {
  return createClearBtnStatus(height.value, weight.value);
});
const inputHeightFeedback = computed(() => {
  return createHeightFeedback(height.value);
});
const inputWeightFeedback = computed(() => {
  return createWeightFeedback(weight.value);
});

// reset data
function clearBtnOnClick(): void {
  height.value = null;
  weight.value = null;
}
</script>

<style scoped>
.NCenter {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  width: 100%;
}
</style>
