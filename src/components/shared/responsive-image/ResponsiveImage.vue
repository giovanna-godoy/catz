<template>
    <img class="img-res" :src="url" :alt="title">
</template>

<script>
export default {
    props: ['url', 'title']
}
</script>

<style>
.img-res {
  width: 100%;
}
</style>