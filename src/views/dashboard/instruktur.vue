<template>
  <div class="container">
    <h2 class="mt-3">Instruktur</h2>

    <div class="d-flex justify-content-center align-items-center">
      <div class="spinner-border text-primary" role="status" v-if="loading==true" id="loading">
        <span class="sr-only">Loading...</span>
      </div>
    </div>

    <div class="card-columns">
      <div class="card" v-for="(element,index) in instruktur" :key="index">
        <div class="card-header">
          <div class="row">
            <div class="col-4 text-center">
              <img
                :src="instruktur.foto"
                width="70"
                height="70"
                class="align-self-start rounded-circle"
              />
            </div>
            <div class="col-6">
              <h5 class="mt-0">{{element.nama}}</h5>
              <span
                v-for="(object,k) in element.programkursusinstrukturs"
                :key="k"
                class="my-2 mx-1"
              ><b-badge pill variant="info">{{object.programkursuses.nama}} </b-badge></span>
            </div>
          </div>
        </div>
        <div class="media-body">
          <div class="mt-3 mx-3">
            <span>
              <b-icon icon="envelope-fill"></b-icon>
              {{element.email}}
            </span>
            <br />
            <span>
              <b-icon icon="geo-alt"></b-icon>
              {{element.alamat_lengkap}}
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "@/service/axios";
export default {
  data: () => {
    return {
      instruktur: [],
      loading: false,
      program: null,
    };
  },
  mounted() {
    this.getinstruktur();
  },
  methods: {
    getinstruktur() {
      this.loading = true;
      axios.get("/frontoffice/instruktur").then((response) => {
        if (response.data.success == true) {
          this.instruktur = response.data.data;
          this.loading = false;
        }
      });
    },
  },
};
</script>

<style>
</style>
