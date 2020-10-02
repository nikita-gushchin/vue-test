<template>
  <div id="app">
    <Subreddits />
  </div>
</template>

<script>
import Subreddits from './components/Subreddits';

export default {
  name: "App",
  data() {
    return {

    }
  },
  
  components: {
    Subreddits,
  },
};
</script>

<style scoped lang="scss">
#app {
  display: flex;
  width: 100%;
}
</style>
