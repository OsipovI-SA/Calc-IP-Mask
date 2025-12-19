<script setup lang="ts">
import {ref} from 'vue'

import {options} from './options'
import {isIpValid, getNetworkAdress,getAddressesCount} from './functions'
function showResult() {
  isShowResult.value = true

}

const ip = ref('')
const mask = ref(options[0])
const isShowResult =ref(false)

</script>

<template>
  <form @submit.prevent="showResult" class="form">
  <input v-model = "ip"/>

  <select v-model="mask">
    <option v-for="option in options" :key="option" :value="option">
      {{option}}
    </option>
  </select>
  
  <button type="submit" :disabled="!isIpValid(ip)">Расчет Ильи </button>
  </form>

<div v-if="isShowResult && isIpValid(ip)" class="result">
  <div>IP: {{ip}}</div>
  <div>Маска подсети: {{mask}}</div>
  <div>Адрес сети: {{getNetworkAdress(ip,mask)}}</div>
  <div>Количество адресов: {{getAddressesCount(mask)}}</div>
  </div>
  </template>

  <style>
  .form {
    display: flex;
    gap: 4px;
  }

  .result{
    border: 1px red;
    border-radius: 16px;
    padding: 16px;
    margin-top: 32px;
    background-color: beige;
  }
  </style>