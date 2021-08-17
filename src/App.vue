<template>
  <div class="general">
    <router-view></router-view>
  </div>
</template>

<script>
import Panel from "./components/shared/panel/Panel.vue";
import ResponsiveImage from "./components/shared/responsive-image/ResponsiveImage.vue";

export default {
  components: {
    'Panel': Panel,
    'ResponsiveImage': ResponsiveImage
  },
  data() {
    return {
      title: 'Picz',
      photos: [],
      filter: ''
    }
  },
  computed: {
    filteredPhotos() {
      if (this.filter) {
        let exp = new RegExp(this.filter.trim(), 'i');
        return this.photos.filter(photo => exp.test(photo.title));
      } else {
        return this.photos;
      }
    }
  },
  created() {
    this.$http.get('http://localhost:3000/v1/photos')
      .then(res =>res.json())
      .then(photos => this.photos = photos, err => console.log("ERROR"))
  },
}
</script>

<style>
.general {
  font-family: Helvetica, sans-serif;
  margin: 0 auto;
  width: 96%;
}
</style>
