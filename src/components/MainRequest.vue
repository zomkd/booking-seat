<script setup lang="ts">
import { ref } from "vue";
import "../assets/main.scss";

const name = ref("");
const surname = ref("");
let guests = [ 
  {fullname: 'демидов никита', table: '1'},
]
let table = ref('')
let isFind = ref(false)
function findTable() {
  isFind.value = true
  let fullname: string = surname.value + ' ' + name.value
  let chosenTable: any | string = guests.find(e => e.fullname === fullname.toLowerCase())?.table
  if (chosenTable === undefined) {
    table.value = "Вас нет в списке, попробуйте еще раз"
  }
  else {table.value = 'Ваше место под номером: ' + chosenTable}
}
</script>

<template lang="pug">
.main
  .order__header(v-if="!isFind")
    h2 Введите данные
    .input__name
      label Имя
      input(type="text" v-model="name")
    .input__surname
      label Фамилия
      input(type="text" v-model="surname")

    button(type='button' @click="findTable") Старт
  .success(v-else)
    .p {{ table}}
    button(class="exit__button" type='button' @click="isFind = false") Назад
</template>

