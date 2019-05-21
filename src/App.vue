<template>
  <div id="q-app">
 <div  class="bg-brand" text-white>
    <router-view />
     </div>
  </div>
</template>

<script>
export default {
  name: 'App',
    mounted() {
    window.onresize = () => {
      console.log("app onresize");
      return (() => {

      })();
    };
  }
}
</script>

<style>
.text-brand {
  color: #F7F9FA;
}
.bg-brand {
  background: #F2F2F2;
}
</style>
