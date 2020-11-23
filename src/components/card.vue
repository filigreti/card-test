<template>
  <main>
    <div class="bg-white big-rounded width-size">
      <div class="flex px-10 py-8 border-b justify-between items-center">
        <div>
          <h2 class="text-base font-bold">Overall Rating</h2>
          <div class="text-green-600 mt-1 flex items-center">
            <h1 class="text-lg pr-2">{{ cardResult.dob.age }}</h1>
            <div
              @mouseover="hoverState(i)"
              @mouseleave="currentHover = null"
              @click="getStar(i)"
              v-for="i in 5"
              :key="i"
              class="ml-1 text-gray-300 star-hover"
              :class="{
                'text-green-600': i <= currentHover || i <= currentStar,
              }"
            >
              <div class="flex items-center">
                <svg
                  class="w-3 h-3 fill-current"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 -10 511.98685 511"
                >
                  <path
                    d="m510.652344 185.902344c-3.351563-10.367188-12.546875-17.730469-23.425782-18.710938l-147.773437-13.417968-58.433594-136.769532c-4.308593-10.023437-14.121093-16.511718-25.023437-16.511718s-20.714844 6.488281-25.023438 16.535156l-58.433594 136.746094-147.796874 13.417968c-10.859376 1.003906-20.03125 8.34375-23.402344 18.710938-3.371094 10.367187-.257813 21.738281 7.957031 28.90625l111.699219 97.960937-32.9375 145.089844c-2.410156 10.667969 1.730468 21.695313 10.582031 28.09375 4.757813 3.4375 10.324219 5.1875 15.9375 5.1875 4.839844 0 9.640625-1.304687 13.949219-3.882813l127.46875-76.183593 127.421875 76.183593c9.324219 5.609376 21.078125 5.097657 29.910156-1.304687 8.855469-6.417969 12.992187-17.449219 10.582031-28.09375l-32.9375-145.089844 111.699219-97.941406c8.214844-7.1875 11.351563-18.539063 7.980469-28.925781zm0 0"
                  />
                </svg>
              </div>
            </div>
            <div class="text-gray-500 text-sm ml-4 pt-1">{{ votes }} Votes</div>
          </div>
        </div>
        <div
          class="text-green-600 cursor-pointer h-12 w-12 rounded-lg flex items-center justify-center bg-gray-200"
        >
          +
        </div>
      </div>
      <div class="py-6 px-10">
        <div class="mt-2 flex">
          <img
            :src="cardResult.picture.thumbnail"
            class="w-12 rounded-lg object-cover h-12 cursor-pointer"
            alt=""
          />
          <div class="ml-4 mb-1 flex flex-col justify-between">
            <h1 class="pb-1 font-black">
              {{ cardResult.name.first }} {{ cardResult.name.last }}
            </h1>
            <div class="flex text-gray-500 text-sm items-center">
              <span class="">{{ cardResult.dob.age }} yrs</span>

              <!-- <div v-for="i in 5" :key="i">
                <div class="flex items-center">
                  <svg
                    :class="{ 'text-green-600': i <= 3 }"
                    class="w-3 h-3 fill-current mr-1"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 -10 511.98685 511"
                  >
                    <path
                      d="m510.652344 185.902344c-3.351563-10.367188-12.546875-17.730469-23.425782-18.710938l-147.773437-13.417968-58.433594-136.769532c-4.308593-10.023437-14.121093-16.511718-25.023437-16.511718s-20.714844 6.488281-25.023438 16.535156l-58.433594 136.746094-147.796874 13.417968c-10.859376 1.003906-20.03125 8.34375-23.402344 18.710938-3.371094 10.367187-.257813 21.738281 7.957031 28.90625l111.699219 97.960937-32.9375 145.089844c-2.410156 10.667969 1.730468 21.695313 10.582031 28.09375 4.757813 3.4375 10.324219 5.1875 15.9375 5.1875 4.839844 0 9.640625-1.304687 13.949219-3.882813l127.46875-76.183593 127.421875 76.183593c9.324219 5.609376 21.078125 5.097657 29.910156-1.304687 8.855469-6.417969 12.992187-17.449219 10.582031-28.09375l-32.9375-145.089844 111.699219-97.941406c8.214844-7.1875 11.351563-18.539063 7.980469-28.925781zm0 0"
                    />
                  </svg>
                </div>
              </div> -->
              <!-- <div class="text-gray-500 text-sm ml-4 pt-1">6 days ago</div> -->
            </div>
          </div>
        </div>
        <div class="mt-4 text-gray-500">
          <div>{{ cardResult.email }}</div>
          <div class="tracking-wider pt-x leading-7">{{ cardResult.cell }}</div>
        </div>
        <div class="mt-6 pb-4 text-gray-500">
          {{ moment(cardResult.dob.date).format("ll") }}
          <!-- <span class="pl-2">|</span> -->
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import moment from 'moment'
export default {
  props: ['results'],
  data() {
    return {
      moment,
      currentStar: null,
      currentHover: null
    }
  },
  computed: {
    cardResult() {
      return this.results
    },
    votes() {
      return this.currentStar !== null ? (this.results.dob.age + this.currentStar) : this.results.dob.age
    }
  },
  methods: {
    getStar(i) {
      this.currentStar = i
    },
    hoverState(i) {
      this.currentHover = i
    }
  }

};
</script>

<style>
.width-size {
  width: 22rem;
}
.big-rounded {
  border-radius: 15px;
}
.star-hover:hover {
  color: #049669;
}
</style>