<template>
  <div class="general">
    <nav>
      <ul>       
          <li v-for="route in routes" :key="route.title">
            <router-link :to="route.path ? route.path : '/'">{{route.title}}</router-link>
          </li>
      </ul>
    </nav>

    <router-view></router-view>
  </div>
</template>

<script>
import { routes }  from './routes';

export default {
  data() {
    return {
      routes
    }
  }
}
</script>

<style>
.general {
  font-family: Helvetica, sans-serif;
  margin: 0 auto;
  width: 96%;
}
</style>
