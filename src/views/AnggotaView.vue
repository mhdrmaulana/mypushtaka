<template>
  <div class="container">
    <h1 class="card-title">List Anggota</h1>
    <div class="card card-header mb-1 col-10" v-for="(data, index) in anggota" :key="data.id">
      <div class="container-card bg-white-box">
        <h2>{{ data.nama }}</h2>
        <div class="container-card bg-green-box mb-1 col-10">
          <h4>Nomor : {{ data.nomor }}</h4>
          <ul>
            <li>
              <p>Alamat : {{ data.alamat }}</p>
              <p>Jenis Kelamin : {{ data.jenis_kelamin }}</p>
              <p>No.HP : {{ data.no_hp }}</p>
            </li>
            <div class="card-body">
              <router-link class="button-edit" :to="`/edit-anggota/${data.nomor}`">Edit</router-link>
              <button class="button-delete" role="button" @click="hapusAnggota(data.kode)">Delete</button>
            </div>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
  data() {
    return {
      anggota: []
    };
  },
  mounted() {
    this.getAnggotaList();
  },
  methods: {
    getAnggotaList() {
      axios.get('http://localhost/mypustaka/select_anggota.php')
          .then(response => {
            this.anggota = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    hapusAnggota(nomor) {
      axios.delete(`http://localhost/mypustaka/delete_anggota.php/${nomor}`)
          .then(response => {
            console.log(response.data);
            this.getAnggotaList();
          })
          .catch(error => {
            console.log(error);
          });
    }
  }
};
</script>

<style>

body {
  background-color: black;
}

.container {
  width: 1200px;
  padding: 0;
  margin-right: auto;
  margin-left: auto;
}

.card {
  color: white;
  max-width: 550px;
  border: 0;
  width: 50%;
  float: left;
  margin-right: 30px; /* Menambahkan jarak horizontal antara kolom */
  margin-bottom: 30px; /* Menambahkan jarak vertikal antara kolom */
}

.container-card {
  position: relative;
  border: 2px solid transparent;
  background: linear-gradient(71deg, #080509, #1a171c, #080509);
  background-clip: padding-box;
  border-radius: 45px;
  padding: 40px;
}


.card-title {
  margin-top: 30px;
  margin-bottom: 30px;
  font-weight: 600;
  color: white;
  letter-spacing: -0.02em;
  line-height: 40px;
  font-style: normal;
  font-size: 50px;
  padding-bottom: 8px;
  text-align: center;
}

.button-edit {
  align-items: center;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: transparent 0 0 0 3px, rgba(18, 18, 18, .1) 0 6px 20px;
  box-sizing: border-box;
  color: #121212;
  cursor: pointer;
  display: inline-flex;
  flex: 1 1 auto;
  font-family: Inter, sans-serif;
  font-size: 1.2rem;
  font-weight: 700;
  justify-content: center;
  line-height: 1;
  margin: 0;
  outline: none;
  padding: 1rem 1.2rem;
  text-align: center;
  text-decoration: none;
  transition: box-shadow .2s, -webkit-box-shadow .2s;
  white-space: nowrap;
  border: 0;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  float: left; /* Menambahkan float left */
}

.button-edit:hover {
  box-shadow: #121212 0 0 0 3px, transparent 0 0 0 0;
}

.button-delete {
  align-items: center;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: transparent 0 0 0 3px, rgba(18, 18, 18, .1) 0 6px 20px;
  box-sizing: border-box;
  color: #121212;
  cursor: pointer;
  display: inline-flex;
  flex: 1 1 auto;
  font-family: Inter, sans-serif;
  font-size: 1.2rem;
  font-weight: 700;
  justify-content: center;
  line-height: 1;
  margin: 0;
  outline: none;
  padding: 1rem 1.2rem;
  text-align: center;
  text-decoration: none;
  transition: box-shadow .2s, -webkit-box-shadow .2s;
  white-space: nowrap;
  border: 0;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  float: right; /* Menambahkan float right */
}

.button-delete:hover {
  box-shadow: #121212 0 0 0 3px, transparent 0 0 0 0;
}

</style>
