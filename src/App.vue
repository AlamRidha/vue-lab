<template>
  <div>
    <h1>Declarative Rendering</h1>
    <p>{{ namaVariabel }}</p>
    <p>{{ namaVariabel2 }}</p>
    <p>{{ namaVariabel3 }}</p>
    <p>{{ variabelReactive }}</p>
    <p>{{ variabelReactive }}</p>

    <h1>Attribute Rendering</h1>
    <p v-bind:class="styleParagraf">Hallo</p>
    <h3 v-bind:class="styleParagraf">Hallo</h3>
    <h5 v-bind:class="styleParagraf">Hallo</h5>

    <hr>

    <h1>Event Listener</h1>
    <p>{{ data }}</p>
    <button @click="increment">Tambah</button>
    <button @click="decrement">Kurang</button>

    <h1>Form Binding</h1>
    <form action="">
      <input type="text" v-model="username"><br>
      <input type="password" v-model="password">
    </form>
    <p>Hasil dari form : {{ username }} dan password {{ password }}</p>
  </div>
</template>

<!-- vue 3 -->
<script setup>
import { ref, reactive } from 'vue'

const username = ref("")
const password = ref("")


const data = ref(0)

function increment() {
  data.value++
}

function decrement() {
  data.value--
}

const styleParagraf = ref("paragraf")

// ref bisa untuk semua tipe nilai, string,int, array, object, array object
const namaVariabel = ref("hello vue")
const namaVariabel2 = ref(1)
const namaVariabel3 = ref([{
  nama: "PBK",
  kelas: "Praktikum"
}])

// reactive didesain untuk object, array object
const variabelReactive = reactive({
  nama: "PBK 2",
  kelas: "Praktikum",
  kode: 9
})

</script>

<style scoped>
.paragraf {
  font-size: 25px;
  color: red;
}
</style>
