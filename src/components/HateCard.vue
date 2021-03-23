<template>
  <div>

    <b-jumbotron>
      <template #header>Asian Hate Speech</template>

      <template #lead>
        This is a simple hero statistic that tells us the percentage of hate speech on 4chan
      </template>

      <hr class="my-4">

      <p>
        It uses high level machine learning.
      </p>

      <b-card
      header="Asian Hate Speech"
      header-text-variant="white"
      header-tag="header"
      header-bg-variant="dark"
      footer="Data By Joyce"
      footer-tag="footer"
      footer-bg-variant="success"
      footer-border-variant="dark"
      title="Percentage"
      style="max-width: 20rem;"
      >
      <b-spinner v-if="loadingStatus" variant="primary" label="Spinning"></b-spinner>
      <b-card-text v-else>
        {{ percentage }}
      </b-card-text>
    </b-card>


    <b-button variant="primary" @click="getHateSpeechPercentage">Update Data</b-button>
  </b-jumbotron>
</div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'HateCard',
    data() {
      return {
        loadingStatus: true,
        percentage: 0.0
      }
    },
    mounted() {
      this.getHateSpeechPercentage();
    },
    methods: {
      getHateSpeechPercentage() {
        this.loadingStatus = true;
        const path = 'http://127.0.0.1:5000/get_hate';
        axios.get(path)
        .then((res) => {
          this.percentage = res.data.percentage;
          this.loadingStatus = false;
        })
        .catch((error) => {
          console.error(error);
          this.percentage = -1.0;
          this.loadingStatus = false;
        });
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
