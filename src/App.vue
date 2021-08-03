<template>
  <div class="general">
    <h1 class="title">{{ title }}</h1>
    <input type="search" class="filter" v-on:input="filter = $event.target.value" placeholder="Filtre pelo título da foto">
    <ul class="photo-list">
      <li class="photo-list-item" v-for="photo in filteredPhotos"  v-bind:key="photo.id">
        <Panel :title="photo.title">
            <ResponsiveImage :url="photo.url" :title="photo.title"/>
        </Panel>
      </li>
    </ul>
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

.title {
  font-family: Arial, Helvetica, sans-serif;
}

.photo-list {
  list-style: none;
}

.photo-list .photo-list-item {
  display: inline-block;
}

.title {
  text-align: center;
}

.filter {
  display: block;
  width: 100%;
}
</style>
