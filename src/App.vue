<script setup>
import { ref } from 'vue'
import axios from 'axios'

const url = import.meta.env.VITE_URL
const dataList = ref([])
const sel = ref('請稍後取得資料中')
const optionTag = ref('')

axios.get(url).then((res) => {
  dataList.value = res.data.data.XML_Head.Infos.Info
  sel.value= '景點資料'
})
</script>

<template>
  <div class="img">
    <h2 class="text-center text-primary">高雄景點資訊</h2>
    <select  class="mt-2 text-secondary" v-model="optionTag">
      <option disabled selected value="">{{ sel }}</option>
        <option :value="data" v-for="data in dataList"  :key="data.Name">
          {{ data.Name }}
        </option>
    </select>
  </div>
  <div class="container mt-5">
    <div class="row">
      <div class="col-lg-4">
        <div class="div text-secondary">
          <h5 class="h5" style="font-weight: 500">地點名稱:{{ optionTag.Name }}</h5>
          <h6 class="h6 mt-lg-3 mt-3" style="font-weight: 400">地址:{{ optionTag.Add }}</h6>
          <h6 class="h6 mt-lg-3 mt-3" style="font-weight: 400">介紹:{{ optionTag.Toldescribe }}</h6>
        </div>
      </div>
      <div class="col-lg-8">
        <div style="width: 100%; height: 100%" class="mt-5 mt-xl-0">
          <iframe
            :src="`https://maps.google.com.tw/maps?f=q&hl=zh-TW&geocode=&q=${optionTag.Py},${optionTag.Px}(${optionTag.Name})&z=16&output=embed`"
            loading="lazy"
            width="100%"
            height="100%"
          >
          </iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
select {
  outline: none;
  padding: 3px 10px;
  border-radius: 5px;
}
.img {
  background-image: url('../public/bgc.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center top;
  width: 100%;
  height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
select {
  width: 30%;
}
option {
  width: 50%;
}
</style>
