<template>
  <div id="app">
    <!-- <div >
        <card :results="result" />
    </div> -->
    <div
      v-for="(result, index) in results"
      :key="index"
      :class="{ 'bg-gray-700': bgChange }"
      class="flex w-100 h-screen bg-gray-200 justify-center items-center"
    >
      <card @colorChange="changeColor" :results="result" />
    </div>
  </div>
</template>

<script>
import card from "@/components/card.vue";

export default {
  name: "App",
  data() {
    return {
      results: [],
      bgChange: false
    };
  },
  components: {
    card,
  },
  methods: {
    async makeCall() {
      let response = await fetch("https://randomuser.me/api");
      let user = await response.json();
      this.results = user.results;
    },
    changeColor() {
      this.bgChange = true
    }
  },
  async created() {
    await this.makeCall();
  },
};
</script>




<style>
#app {
  font-family: "Lato", sans-serif !important;
}
</style>
