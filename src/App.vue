<template>
  <div style="width:100%">
    <table style="width:inherit;">
        <caption>Descrepencies checker between languages files </caption>
        <thead>
            <tr>
              <th>#</th>
              <th>Keys</th>
              <th>en</th>
              <th>ms</th>
              <th>zh</th>
              <th>zh-CN</th>
            </tr>
        </thead>
        <tbody>
          <tr v-for="(value, key, index) in objVfor" :key="index">
            <td style="text-align: center;">{{ index }}</td>
            <td>{{ key }}</td>

            <td v-if="value['en']">{{ value['en'] }}</td>
            <td v-else style="background-color: lightpink;"> falsy value </td>

            <td v-if="value['ms']">{{ value['ms'] }}</td>
            <td v-else style="background-color: lightpink;"> falsy value </td>

            <td v-if="value['zh']">{{ value['zh'] }}</td>
            <td v-else style="background-color: lightpink;"> falsy value </td>

            <td v-if="value['zh-CN']">{{ value['zh-CN'] }}</td>
            <td v-else style="background-color: lightpink;"> falsy value </td>
          </tr>
        </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import enjs from './lang/en'
import msjs from './lang/ms'
import thjs from './lang/th'
import zhCNjs from './lang/zh-CN'
import zhjs from './lang/zh'

const enKeys = Object.keys(enjs)
const objVfor = ref()
let temporary = {}
enKeys.forEach((str, ind)=> {
  if(typeof enjs[str] === 'object') {
    let nested = Object.keys(enjs[str])
    nested.forEach((nestedKey, ind)=>{
      let enKeyObj = enjs[str] || {}
      let msKeyObj = msjs[str] || {}
      let zhKeyObj = zhjs[str] || {}
      let zhCNKeyObj = zhCNjs[str] || {}
      let tempKey = '"' + str + '.' + nestedKey + '"'

      temporary[tempKey] = {
        'en': enKeyObj[nestedKey],
        'ms': msKeyObj[nestedKey],
        'zh': zhKeyObj[nestedKey],
        'zh-CN': zhCNKeyObj[nestedKey],
      }
      // console.log(temporary);
    })
  } else {
    temporary[str]= {
      'en': enjs[str],
      'ms': msjs[str],
      'zh': zhjs[str],
      'zh-CN': zhCNjs[str],
    }
  }
})
objVfor.value = temporary
console.log('objVfor.value', objVfor.value)


</script>

<style>
tr {
  border: 1px solid lightgray;
}
th {
  font-weight: bold;
}
th, td {
  border: 1px solid lightgray;
  padding: 0.5rem;
}
</style>