<template>
  <div>
    <Header/>
    <Banner/>
    <Main/>
  </div>
</template>

<script>
import Banner from './components/Banner.vue';
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name : 'Home',
  components : {
    Banner,
    Header,
    Main
  } 
}
</script>

