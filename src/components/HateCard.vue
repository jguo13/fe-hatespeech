<template>
  <div>
    <b-card
    header="Hate Speech"
    header-text-variant="white"
    header-tag="header"
    header-bg-variant="dark"
    footer="Card Footer"
    footer-tag="footer"
    footer-bg-variant="success"
    footer-border-variant="dark"
    title="Percentage"
    style="max-width: 20rem;"
    >
    <b-card-text>{{ percentage }}</b-card-text>
  </b-card>
</div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'HateCard',
    data() {
      return {
        percentage: 0.0
      }
    },
    method: {
      getHateSpeechPercentage() {
        const path = '127.0.0.1:5000/books';
        axios.get(path)
        .then((res) => {
          this.percentage = res.data.percentage;
        })
        .catch((error) => {
          console.error(error);
        });
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
