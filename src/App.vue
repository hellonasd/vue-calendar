<template>
  
  <app-calendar></app-calendar>
</template>

<script>
import AppCalendar from "./components/AppCalendar.vue";


export default {
  name: "App",
  components: { AppCalendar },
};
</script>

<style lang="scss">
*{
  padding: 0;
  margin: 0;
}
</style>
