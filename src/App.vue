<template>
  <div id="app">
    <!-- <div >
        <card :results="result" />
    </div> -->
    <div
      v-for="(result, index) in results"
      :key="index"
      class="flex w-100 h-screen bg-gray-200 justify-center items-center"
    >
      <card :results="result" />
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
