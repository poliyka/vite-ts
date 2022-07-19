<template>
  <NConfigProvider :theme="darkTheme">
    <NCard title="BMI計算器" :contentStyle="nCardContentStyle" :headerStyle="nCardHeaderStyle">
      <BMI />
      <table
        align="center"
        border="1"
        cellspacing="0"
        bordercolordark="black"
        bordercolorlight="black"
        height="159"
        width="100%"
      >
        <tbody>
          <tr bordercolor="#cccccc" bgcolor="#1a936f">
            <td width="30%" height="35"></td>
            <td width="70%" height="35">
              <div align="center">
                <font color="#000000"
                  ><span class="01">身體質量指數(BMI)<br />(kg/m2)</span><br
                /></font>
              </div>
            </td>
          </tr>
          <tr bordercolor="#cccccc">
            <td class="01" width="30%">
              <div align="center">體重過輕</div>
            </td>
            <td class="01" width="70%">
              <div align="center">BMI ＜ 18.5</div>
            </td>
          </tr>
          <tr bordercolor="#cccccc">
            <td class="01" width="30%">
              <div align="center">正常範圍</div>
            </td>
            <td class="01" width="70%">
              <div align="center">18.5≦BMI＜24</div>
            </td>
          </tr>
          <tr bordercolor="#cccccc">
            <td class="01" width="30%">
              <div align="center">異常範圍</div>
            </td>
            <td valign="top" width="70%">
              <div align="center">
                <span class="01"
                  >過重：24≦BMI＜27<br />輕度肥胖：27≦BMI＜30<br />中度肥胖：30≦BMI＜35<br />重度肥胖：BMI≧35</span
                >
                <br />
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </NCard>
  </NConfigProvider>
</template>

<script lang="ts" setup>
import BMI from "@/components/BMI.vue";
import { NCard } from "naive-ui";
import { NConfigProvider, createTheme, inputDark, buttonDark, cardDark, formDark } from "naive-ui";

// theme
const darkTheme = createTheme([inputDark, buttonDark, cardDark, formDark]);

const nCardContentStyle = "background-color: #22223a";
const nCardHeaderStyle = "background-color: #4a4e68";
</script>
