<template>
  <NConfigProvider :theme="darkTheme">
    <NCard title="BMI計算器" :contentStyle="nCardContentStyle" :headerStyle="nCardHeaderStyle">
      <BMI />
      <BMIDetailTableVue />
    </NCard>
  </NConfigProvider>
</template>

<script lang="ts" setup>
import BMI from "@/components/BMI.vue";
import BMIDetailTableVue from "@/components/BMIDetailTable.vue";
import { NCard } from "naive-ui";
import { NConfigProvider, createTheme, inputDark, buttonDark, cardDark, formDark } from "naive-ui";

// theme
const darkTheme = createTheme([inputDark, buttonDark, cardDark, formDark]);

const nCardContentStyle = "background-color: #22223a";
const nCardHeaderStyle = "background-color: #4a4e68";
</script>
