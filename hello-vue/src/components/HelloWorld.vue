<script setup lang="ts">
import { ref, computed, reactive } from 'vue'

//リスト3-2
//テンプレート変数　＝　ref関数
const name = ref('田中太郎')

//リスト3-3
const now = new Date()
const nowStr = now.toLocaleTimeString()

const timeStrRef = ref(nowStr)

function changeTime(): void {
  const newTime = new Date()
  const newTimeStr = newTime.toLocaleTimeString()

  timeStrRef.value = newTimeStr
}

setInterval(changeTime, 1000)

//リスト3-4
const radiusInit = Math.round(Math.random() * 10)
const PI = ref(3.14)
const radius = ref(radiusInit)

//算出プロパティ（読み取り専用）
const area = computed((): number => {
  return radius.value * radius.value * PI.value
})

setInterval((): void => {
  radius.value = Math.round(Math.random() * 10)
}, 1000)

//リスト3-5
const data = reactive({
  PI_2: 3.14,
  radius_2: Math.round(Math.random() * 10),
})

const area_2 = computed((): number => {
  return data.radius_2 * data.radius_2 * data.PI_2
})

setInterval((): void => {
  data.radius_2 = Math.round(Math.random() * 10)
}, 1000)
</script>

<template>
  //マスタッシュ構文
  <h1>こんにちは！{{ name }}さん！</h1>

  <p>現在時刻 ref: {{ timeStrRef }}</p>

  <p>半径{{ radius }}の円の面積を円周率{{ PI }}で計算すると、{{ area }}</p>

  <p>半径{{ data.radius_2 }}の円の面積を円周率{{ data.PI_2 }}で計算すると、{{ area_2 }}</p>
</template>
