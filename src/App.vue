<template>
  <header>
    <Header />
  </header>

  <div class="isi" :style="(!show) ? 'display:block' : 'display:none'">
    <div class="text">
      <h3>Silahkan Tempelkan Kartu Smart Presensi Anda</h3>
    </div>
    <div class="foto">
      <img src="@/assets/tap-card-logo.png" alt="image" class="tap-card">
    </div>
  </div>

  <div class="container2 p-0 mt-5 container-response" :style="(show) ? 'display:block' : 'display:none'">
    <div class="container container-response-2">
      <div class="container-response-3">
        <video loop="true" autoplay="autoplay" style="width: 20rem;" class="video">
          <source src="@/assets/hai.mp4" type="video/mp4" class="mp4">
          <source src="@/assets/hai.ogg" type="video/ogg" class="ogg">
        </video>
        <h3 class="text-center text-response h3-nih"></h3>
      </div>
    </div>
  </div>

  <div class="rfid">
    <input type="text" name="" class="input-rfid" autofocus>
    <!-- <div class="tiban"></div> -->
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
  text-align: center;
}

.container-response-2 {
  min-width: 70vw;
  display: flex;
  justify-content: center;
}

.container-response-3 {
  width: 50rem;
  text-align: center;
  height: 0;
  padding-bottom: 30%;
  position: relative;
}
</style>

<script setup>
import Header from './components/Header.vue';
import { onMounted, ref } from 'vue';
import axios from 'axios';

const response = ref([]);
let detik = 0;
let show = ref(false);

const hitungDetik = function () {
  detik++;
  if (detik == 15) {
    show.value = false;
    detik = 0;
    response.value = [];
  } else if (detik <= 15 && show.value) {
    setTimeout(() => {
      hitungDetik();
    }, 1000);
  }
};

onMounted(() => {
  const inputRfid = document.querySelector('.input-rfid');
  let mp4 = document.querySelector('.container-response video');
  let ogg = document.querySelector('.container-response .ogg');
  let textResponse = document.querySelector('.container-response .text-response');

  inputRfid.addEventListener('change', function (e) {
    if (detik <= 15) {
      detik = 0;
      show.value = false;
      fetch(e);
    } else {
      fetch(e);
    }
  })

  const fetch = function (e) {
    axios.post('http://localhost:8000/api/absen', {
      rfid: e.target.value
    }).then((response) => {
      console.log(response)
      if (!show.value) {
        show.value = true;
        hitungDetik();
      }
      response.value = response.data;

      if (response.data.kode_respon == '1') {
        mp4.setAttribute('src', '/src/assets/hai.mp4');
        ogg.setAttribute('src', '/src/assets/hai.ogg');
        textResponse.innerHTML = `${response.data.user.name} berhasil presensi`;
      } else {
        mp4.setAttribute('src', '/src/assets/hai.mp4');
        ogg.setAttribute('src', '/src/assets/hai.ogg');
        textResponse.innerHTML = `Hati hati dijalan ${response.data.user.name}`;
      }

      inputRfid.value = '';
    }).catch(function (error) {
      if (!show.value) {
        show.value = true;
        hitungDetik();
      }
      response.value = error.response.data;

      if (error.response.data.kode_respon == '4' || error.response.data.kode_respon == '6' || error.response.data.kode_respon == '7' || error.response.data.kode_respon == '8' || error.response.data.kode_respon == '9') {
        mp4.setAttribute('src', '/src/assets/telat.mp4');
        ogg.setAttribute('src', '/src/assets/telat.ogg');

        if (error.response.data.kode_respon == '4') {
          textResponse.innerHTML = `Maaf, kamu terlambat. <br> Silahkan lapor ke guru piket untuk data absensi kamu hari ini. Jangan terlambat lagi lain kali yaa!`;
        } else if (error.response.data.kode_respon == '6') {
          textResponse.innerHTML = `Maaf, agenda tidak tersedia. <br> Silahkan lapor ke guru piket.`;
        } else if (error.response.data.kode_respon == '7') {
          textResponse.innerHTML = `Maaf, kartu absensi anda tidak aktif. <br> Silahkan lapor ke guru piket.`;
        } else if (error.response.data.kode_respon == '8') {
          textResponse.innerHTML = `Maaf, kartu absensi tidak ditemukan. <br> Silahkan lapor ke guru piket.`;
        } else {
          textResponse.innerHTML = `Tidak ada kegiatan disekolah pada hari minggu. <br> Silahkan nikmati waktu liburmu yaa!`;
        }
      } else if (error.response.data.kode_respon == '5') {
        mp4.setAttribute('src', '/src/assets/belumPulang.mp4');
        ogg.setAttribute('src', '/src/assets/belumPulang.ogg');
        textResponse.innerHTML = `Sekarang belum waktunya pulang, silahkan tetap berada di area sekolah sampai waktu pulang tiba yaa!`;
      } else if (error.response.data.kode_respon == '3') {
        mp4.setAttribute('src', '/src/assets/angry.mp4');
        ogg.setAttribute('src', '/src/assets/angry.ogg');
        textResponse.innerHTML = `Kamu sudah absen masuk ataupun pulang, jangan iseng tapping terus menerus yaa!!!`;
      }

      inputRfid.value = '';
    }
    )
  }
})
</script>
