<template>
  
  <header>
    <Header />
  </header>

  <div class="alert alert-success m-4" role="alert" v-if="kode_respon == 4 && show">
    Rfid sudah tidak aktif
  </div>

  <div class="isi" v-if="!kode_respon && !show">
    <div class="foto">
      <img src="@/assets/contactless-payment-credit-card-hand-tap-pay-wave-logo-vector-wireless-nfc-pass-icon-161259873-38930.png" alt="image" style="width: 500px;height: 500px;object-fit: cover;margin-top: 50px;">
    </div>
  </div>
  
  <div class="container1 p-0 mt-5" v-if="kode_respon == 1 && show">
    <div class="isi">
      <div class="foto">
        <div v-if="siswa.profil">
          <img :src="'http://127.0.0.1:8000' + siswa.profil" alt="image" 
            style="width: 300px;height: 300px;border-radius: 50%;object-fit: cover;" v-if="siswa.profil == '/img/profil.png'">
          <img :src="'http://127.0.0.1:8000/storage/' + siswa.profil" alt="image" 
            style="width: 300px;height: 300px;border-radius: 50%;object-fit: cover;" v-else>
        </div>
        <div v-if="user.profil">
          <img :src="'http://127.0.0.1:8000' + user.profil" alt="image" 
            style="width: 300px;height: 300px;border-radius: 50%;object-fit: cover;" v-if="user.profil == '/img/profil.png'">
          <img :src="'http://127.0.0.1:8000/storage/' + user.profil" alt="image" 
            style="width: 300px;height: 300px;border-radius: 50%;object-fit: cover;" v-else>
        </div>
      </div>
    </div>
    <div class="isi2">
      <div class="data" v-if="role == 'siswa'">
        <p class="nama">{{ siswa.name }}</p>
        <p class="npsn">{{ siswa.npsn }}</p>
        <p class="kelas">{{ kelas.nama }}</p>
        <p class="jurusan">{{ siswa.kompetensi.kompetensi }}</p>
      </div>
      <div class="data" v-if="role == 'guru' || role == 'user'">
        <p class="nama">{{ user.name }}</p>
        <p class="npsn">{{ user.nip }}</p>
      </div>
    </div>

    <!-- table guru -->
    <div class="container mt-5" style="min-width: 70vw;" v-if="role == 'guru'">
      <table class="table table-bordered border-secondary text-center" v-if="agendas.length > 0">
        <thead>
          <tr class="text-white" style="background-color: #3bae9c">
            <th scope="col" colspan="2" rowspan="2">HARI/ KELAS</th>
            <th scope="col" colspan="3" rowspan="2" style="text-transform: capitalize;">{{ hari }}</th>
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
          <tr v-for="no in agendas.length">
            <td scope="row">{{ no }}</td>
            <td>{{ agendas[no - 1].jam_awal.split(':')[0] }}:{{ agendas[no - 1].jam_awal.split(':')[1] }}-{{ agendas[no
                - 1].jam_akhir.split(':')[0]
            }}:{{ agendas[no - 1].jam_akhir.split(':')[1] }}</td>
            <td>{{ agendas[no - 1].mapel }}</td>
            <td style="text-transform: capitalize;">{{ agendas[no - 1].nama_kelas }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- table siswa -->
    <div class="container mt-5" style="min-width: 70vw;" v-if="role == 'siswa'">
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
            <td>{{ agendas[no - 1].jam_awal.split(':')[0] }}:{{ agendas[no - 1].jam_awal.split(':')[1] }}-{{ agendas[no
                - 1].jam_akhir.split(':')[0]
            }}:{{ agendas[no - 1].jam_akhir.split(':')[1] }}</td>
            <td>{{ agendas[no - 1].mapel }}</td>
            <td style="text-transform: capitalize;">{{ agendas[no - 1].guru }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <div class="container2 p-0 mt-5 container-pulang" :style="(kode_respon == 2 && show) ? 'display:block;' : 'display:none;'">
    <!-- v-if="kode_respon == 2" -->
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <div style="width:25rem; height:0; padding-bottom:30%; position:relative;">
        <video loop="true" autoplay="autoplay" class="gif-pulang" style="width: 100%;">
            <source src="@/assets/hai.mp4" type="video/mp4">
            <source src="@/assets/hai.ogg" type="video/ogg">
        </video>
        <h3 class="text-center text-pulang-h3-nih" id="text-pulang">Hati-h datii jalan!</h3>
      </div>
    </div>
  </div>
  
  <div class="container2 p-0 mt-5" :style="(kode_respon == 3 && show) ? 'display:block;' : 'display:none;'" >
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <div style="width: 25rem;">
        <video loop="true" autoplay="autoplay" class="gif-angry" style="width: 100%;">
              <source src="@/assets/angry.mp4" type="video/mp4">
              <source src="@/assets/angry.ogg" type="video/ogg">
          </video>
          <h3 class="text-center text-pulang-h3-nih" id="text-pulang">Anda sudah absen masuk ataupun pulang, jangan iseng tapping terus menerus!!!</h3>
      </div>
    </div>
  </div>

  <div class="container2 p-0 mt-5" :style="(kode_respon == 4 && show) ? 'display:block;' : 'display:none;'" >
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <div style="width: 25rem;">
        <video loop="true" autoplay="autoplay" class="gif-telat" style="width: 100%;">
              <source src="@/assets/telat.mp4" type="video/mp4">
              <source src="@/assets/telat.ogg" type="video/ogg">
          </video>
          <h3 class="text-center text-pulang-h3-nih" id="text-pulang">Maaf, kamu terlambat. Silahkan lapor ke guru piket untuk data absensi kamu hari ini. Jangan terlambat lagi lain kali yaa!</h3>
      </div>
    </div>
  </div>

  <div class="container2 p-0 mt-5" :style="(kode_respon == 5 && show) ? 'display:block;' : 'display:none;'" >
    <div class="container" style="min-width: 70vw; display: flex; justify-content: center; margin-top: 100px;">
      <div style="width: 25rem;">
        <video loop="true" autoplay="autoplay" class="gif-telat" style="width: 100%;">
              <source src="@/assets/telat.mp4" type="video/mp4">
              <source src="@/assets/telat.ogg" type="video/ogg">
          </video>
          <h3 class="text-center text-pulang-h3-nih" id="text-pulang">Maaf, kamu terlambat. Silahkan lapor ke guru piket untuk data absensi kamu hari ini. Jangan terlambat lagi lain kali yaa!</h3>
      </div>
    </div>
  </div>

  <div class="rfid">
    <input type="text" name="" class="input-rfid" autofocus>
    <div class="tiban"></div>
  </div>
</template>

<style scoped>
.rfid {
  margin-top: 5rem;
}

.input-rfid {
  position: absolute;
  margin-top: 5px;
}

.tiban {
  background-color: white;
  color: white;
  width: 100vw;
  height: 10vh;

}

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

.npsn,
.kelas,
.jurusan {
  font-size: 30px;
}

.foto {
  display: flex;
  justify-content: center;
}

#carouselExampleControls {
  margin-top: 50px;
  width: 100vw;
  overflow: hidden;
}

.carousel-item {
  padding: 50px;
}
</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router';
import HelloWorld from './components/HelloWorld.vue';
import Header from './components/Header.vue';
import { onMounted, ref } from 'vue';
import axios from 'axios';
import Hai from './components/Hai.vue';

const kode_respon = ref()
const hari = ref()
const agendas = [];
const siswa = ref([]);
const user = ref([]);
const message = ref();
const role = ref();
const kelas = ref();
const kompetensi = ref();
let detik = 0;
let show = ref(false);

const hitungDetik = function () {
  detik++;
  if (detik == 15) {
    show.value = false;
    detik = 0;
    kode_respon.value = '';
  } else if(detik <= 15 && show.value) {
    setTimeout(() => {
      hitungDetik();
    }, 1000);
  }
};

onMounted(() => {
  // kode_respon.value = 2;
  // show.value = true
  // console.log(document.querySelector('#text-pulang'))
 
  const inputRfid = document.querySelector('.input-rfid');
  inputRfid.addEventListener('change', function (e) {
    if (detik <= 15) {
        detik = 0;
        show.value = false;
        fetch(e);
      }else{
        fetch(e);
      }
  })

  const fetch = function(e){
  axios.post('http://127.0.0.1:8000/api/absen', {
      rfid: e.target.value
    }).then((response) => { 
      console.log(response)
      if (!show.value) {
        show.value = true;
        hitungDetik();
      }
      kode_respon.value = response.data.kode_respon
      message.value = response.data.message
      
      // data user
      
      if (kode_respon.value == 1) {
        if (response.data.siswa) {
          hari.value = response.data.hari;
          siswa.value = response.data.siswa;
          role.value = 'siswa';
          kelas.value = response.data.kelas;
          kompetensi.value = response.data.kompetensi;
          if (response.data.agendas) {
            response.data.agendas.forEach(e => {
              agendas.push(e);
            });
          }
        } else {
          if (response.data.hari) {
            role.value = 'guru'
            hari.value = response.data.hari;
            if (response.data.agendas) {
              response.data.agendas.forEach(e => {
                agendas.push(e);
              });
            }

          } else {
            role.value = 'user'
          }
          user.value = response.data.user;
        }
      }else if(kode_respon.value == 2){
        const textPulang = document.querySelector('.text-pulang-h3-nih');
        textPulang.innerHTML = 'Hati hati dijalan ' + response.data.user.name;
        document.querySelector('.gif-pulang').play();
      }else if(kode_respon.value == 3){
        document.querySelector('.gif-angry').play();
      }
      
      inputRfid.value = '';
    })
} 
})
</script>
