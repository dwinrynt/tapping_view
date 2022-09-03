<template>
  <header>
    <Header />
    <div class="isi">
      <div class="foto">
        <img src="" alt="image">
      </div>
    </div>
  </header>
  <div class="container mt-5" style="min-width: 70vw;" v-if="kode_respon == 1">
    <table class="table table-bordered border-secondary text-center" v-if="agendas.length > 0">
      <thead>
        <tr class="text-white" style="background-color: #3bae9c">
          <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
          <th scope="col" colspan="3" style="text-transform: capitalize;">{{ hari }}</th>
        </tr>
        <tr class="text-white" style="background-color: #3bae9c">
          <th colspan="3">{{ agendas[0].nama_kelas }}</th>
        </tr>
        <tr style="background-color: #7de2d1">
          <th scope="row">JAM-KE</th>
          <th>WAKTU</th>
          <th>MAPEL</th>
          <th>GURU</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="no in agendas.length">
          <!-- {{ agendas[no - 1].jam_awal }} -->
          <td scope="row">{{ no }}</td>
          <td>{{ agendas[no - 1].jam_awal.split(':')[0] }}:{{ agendas[no - 1].jam_awal.split(':')[1] }}-{{ agendas[no - 1].jam_akhir.split(':')[0] }}:{{ agendas[no - 1].jam_akhir.split(':')[1] }}</td>
          <td>{{ agendas[no - 1].mapel }}</td>
          <td style="text-transform: capitalize;">{{ agendas[no - 1].guru }}</td>
        </tr>
      </tbody>
    </table>
  </div>
  <input type="text" name="" class="input-rfid" autofocus>
</template>

<style scoped>
.container {
  min-width: 100vw;
  min-height: 100vh;
  background-color: white;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.isi {
  display: flex;
  justify-content: center;
  margin-top: 100px;
}

.foto {
  width: 300px;
  height: 400px;
  display: flex;
  justify-content: center;
  border: 1px solid black;
}

#carouselExampleControls {
  margin-top: 50px;
  width: 100vw;
  overflow: hidden;
}

.carousel-item {
  padding: 50px;
}

.input-rfid {
  z-index: -1;
}
</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
import Header from './components/Header.vue';
import { onMounted, ref } from 'vue';
import axios from 'axios';

const kode_respon = ref()
const message_kode = ref()
const hari = ref()
const agendas = [];
const siswa = ref([]);
const role = ref();

onMounted(() => {
  const inputRfid = document.querySelector('.input-rfid');
  inputRfid.addEventListener('change', function (e) {
    console.log(e.target.value)
    axios.post('http://127.0.0.1:8000/api/absen', {
      rfid: e.target.value
    }).then((response) => {
      // console.log(response)
      kode_respon.value = response.data.kode_respon
      hari.value = response.data.hari
      message_kode.value = response.data.message
      response.data.agendas.forEach(e => {
        agendas.push(e);
      });
      if (kode_respon.value == 1) {
        if (response.data.siswa) {
          siswa.value = response.data.siswa;
          role.value = 'siswa';
        }else{
          role.value = 'user';
        }
      }
      // agendas.push(response.data.agendas)
      // console.log(response.data.agendas)
      console.log(agendas)
    })
  })
})
</script>
