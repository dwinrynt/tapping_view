<template>
  <header>
    <Header />
    <div class="isi">
      <div class="foto">
        <img src="" alt="image">
      </div>
    </div>
  </header>
  <div class="container">
    <div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel">
      <div class="carousel-inner">
        <div class="carousel-item active">
          <div class="table-responsive">
            <table class="table table-bordered border-secondary text-center">
              <thead>
                <tr class="text-white" style="background-color: #3bae9c">
                  <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
                  <th scope="col" colspan="3">SENIN</th>
                </tr>
                <tr class="text-white" style="background-color: #3bae9c">
                  <th colspan="3">XII RPL 2</th>
                </tr>
                <tr style="background-color: #7de2d1">
                  <th scope="row">JAM-KE</th>
                  <th>WAKTU</th>
                  <th>MAPEL</th>
                  <th>GURU</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td scope="row">1</td>
                  <td>07.15-08.00</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">2</td>
                  <td>08.00-08.45</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">3</td>
                  <td>08.45-09.25</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">4</td>
                  <td>09.25-10.00</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">5</td>
                  <td>10.20-10.55</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">6</td>
                  <td>10.55-11.30</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">7</td>
                  <td>11.30-12.05</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">8</td>
                  <td>12.05-12.40</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <div class="carousel-item">
          <div class="table-responsive">
            <table class="table table-bordered border-secondary text-center">
              <thead>
                <tr class="text-white" style="background-color: #3bae9c">
                  <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
                  <th scope="col" colspan="3">SENIN</th>
                </tr>
                <tr class="text-white" style="background-color: #3bae9c">
                  <th colspan="3">XII RPL 2</th>
                </tr>
                <tr style="background-color: #7de2d1">
                  <th scope="row">JAM-KE</th>
                  <th>WAKTU</th>
                  <th>MAPEL</th>
                  <th>GURU</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td scope="row">1</td>
                  <td>07.15-08.00</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">2</td>
                  <td>08.00-08.45</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">3</td>
                  <td>08.45-09.25</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">4</td>
                  <td>09.25-10.00</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">5</td>
                  <td>10.20-10.55</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">6</td>
                  <td>10.55-11.30</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">7</td>
                  <td>11.30-12.05</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
                <tr>
                  <td scope="row">8</td>
                  <td>12.05-12.40</td>
                  <td>PBO</td>
                  <td>PUGUH RISMADI</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
    </div>
    <input type="text" name="" class="input-rfid" autofocus>
  </div>
</template>

<style scoped>
.container{
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

.input-rfid{
  z-index: -1;
}
</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
import Header from './components/Header.vue';
import {onMounted, ref} from 'vue';
import axios from 'axios';

const kode_respon = ref()
const message_kode = ref()
const hari = ref()
const agenda = ref([])  

onMounted(() => {
  const inputRfid = document.querySelector('.input-rfid');
  inputRfid.addEventListener('change', function(e){
    console.log(e.target.value)
    axios.post('http://127.0.0.1:8000/api/absen', {
      rfid: e.target.value
    }).then((response) => {
      console.log(response)
      kode_respon.value = response.data.kode_respon
      hari.value = response.data.hari 
      message_kode.value = response.data.message
      agenda.value = response.data.agendas
      console.log(kode_respon.value)
      console.log(message_kode.value)
      console.log(hari.value)
      console.log(agenda.value)
    })
  })
})
</script>
