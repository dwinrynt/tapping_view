<template>
  <header>
    <Header />
  </header>
  <Hai />
  <div class="container1 p-0 mt-5" v-if="kode_respon == 1">
    <div class="isi">
      <div class="foto">
        <img src="" alt="image">
      </div>
    </div>
    <div class="isi2">
      <div class="data">
        <p class="nama">Dwi Nuryanto</p>
        <p class="npsn">20229232</p>
        <p class="kelas">XII RPL 2</p>
        <p class="jurusan">RPL</p>
      </div>
    </div>
    <!-- table guru -->
    <div class="container mt-5" style="min-width: 70vw;">
      <table class="table table-bordered border-secondary text-center">
        <thead>
          <tr class="text-white" style="background-color: #3bae9c">
            <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
            <th scope="col" colspan="3" rowspan="2" style="text-transform: capitalize;">Sabtu</th>
          </tr>
          <tr class="text-white" style="background-color: #3bae9c">
          </tr>
          <tr style="background-color: #7de2d1">
            <th scope="row">JAM-KE</th>
            <th>WAKTU</th>
            <th>MAPEL</th>
            <th>Kelas</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td scope="row">1</td>
            <td>07.00-12.30</td>
            <td>PBO</td>
            <td style="text-transform: capitalize;">XII RPL 2</td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- table siswa -->
    <div class="container mt-5" style="min-width: 70vw;" v-if="kode_respon == 1">
      <table class="table table-bordered border-secondary text-center" v-if="agendas.length > 0">
        <thead>
          <tr class="text-white" style="background-color: #3bae9c">
            <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
            <th scope="col" colspan="3" style="text-transform: capitalize;">{{ hari }}</th>
          </tr>
          <tr class="text-white" style="background-color: #3bae9c">
            <th colspan="3">{{ agendas[0].nama_kelas }}XII RPL 2</th>
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
  </div>
  
  <div class="container2 p-0 mt-5" v-if="kode_respon == 2">
    <div class="isi">
      <div class="foto">
        <img src="" alt="image">
      </div>
    </div>
    <div class="isi2">
      <div class="data">
        <p class="nama">Dwi Nuryanto</p>
        <p class="nip">20229232</p>
      </div>
    </div>
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <div style="width:30%; height:0; padding-bottom:30%; position:relative;">
        <Hai />
        <h3 class="text-center">Hati-hati di jalan!</h3>
      </div>
    </div>
  </div>

  <div class="container2 p-0 mt-5" v-if="kode_respon == 3">
    <div class="isi">
      <div class="foto">
        <img src="" alt="image">
      </div>
    </div>
    <div class="isi2">
      <div class="data">
        <p class="nama">Dwi Nuryanto</p>
        <p class="npsn">20229232</p>
        <p class="kelas">XII RPL 2</p>
        <p class="jurusan">RPL</p>
      </div>
    </div>
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <video src=""></video>
    </div>
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
  margin-top: auto 100px;
}

.isi2 {
  display: flex;
  justify-content: center;
}

.data {
  text-align: center;
  line-height: 30px;
  margin-top: 30px;
}

.nama {
  font-size: 50px;
  font-weight: 500;
}

.npsn, .kelas, .jurusan {
  font-size: 30px;
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
import Hai from './components/Hai.vue';
import Hai1 from './components/Hai.vue';

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
