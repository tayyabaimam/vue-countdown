<template>
  <div v-if="displayHours <= 0">
    <CTA />
  </div>
  <div v-if="loaded" class="bg-red-900 w-[100vw] h-[100vh] -ml-16">
    <section
      class="text-base flex justify-center content-center mx-auto text-center text-white pt-10"
    >
      <h5 v-if="displayHours <= 72" class="font-semibold">
        IGNITING A NEW ERA OF PRIVACY
      </h5>
      <h5 v-else-if="displayHours <= 168" class="font-medium">
        IGNITING A NEW ERA OF PRIVACY
      </h5>
      <h5 v-else-if="displayHours <= 480" class="font-light">
        IGNITING A NEW ERA OF PRIVACY
      </h5>
      <h5 v-else class="font-extralight">IGNITING A NEW ERA OF PRIVACY</h5>
    </section>
    <section
      class="flex text-6xl justify-center items-center content-center text-white pt-32"
    >
      <div class="hours mr-2 relative">
        {{ displayHours }}
        <div class="label text-sm absolute bottom-0"></div>
      </div>
      <span class="leading-snug">:</span>
      <div class="minutes mx-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute bottom-0"></div>
      </div>
      <span class="leading-snug">:</span>
      <div class="seconds mx-2 relative">
        {{ displaySeconds }}
        <div class="label text-sm absolute bottom-0"></div>
      </div>
    </section>
    <section>
      <video v-if="displayHours <= 0" autoplay loop muted class="bg-red-900">
        <source src="../assets/1.mp4" type="video/mp4" />
      </video>
      <video
        v-else-if="displayHours <= 72"
        autoplay
        loop
        muted
        class="bg-red-900"
      >
        <source src="../assets/1.mp4" type="video/mp4" />
      </video>
      <video
        v-else-if="displayHours <= 168"
        autoplay
        loop
        muted
        class="bg-red-900"
      >
        <source src="../assets/1.mp4" type="video/mp4" />
      </video>
      <video
        v-else-if="displayHours <= 480"
        autoplay
        loop
        muted
        class="bg-red-900"
      >
        <source src="../assets/1.mp4" type="video/mp4" />
      </video>
      <video v-else autoplay loop muted class="bg-red-900">
        <source src="../assets/1.mp4" type="video/mp4" />
      </video>
    </section>
  </div>
</template>

<script>
import CTA from "./CTA.vue";
export default {
  components: { CTA },
  props: ["year", "month", "date", "hour", "minute", "second", "millisecond"],
  data: () => ({
    displayHours: 0,
    displayMinutes: 0,
    displaySeconds: 0,
    loaded: false,
  }),
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60;
    },
    _hours() {
      return this._minutes * 60;
    },
    end() {
      return new Date(
        this.year,
        this.month,
        this.date,
        this.hour,
        this.minute,
        this.second,
        this.millisecond
      );
    },
  },
  mounted() {
    this.showRemaining();
  },
  methods: {
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        //const end = new Date(2023, 6, 20, 12, 0, 0);
        const distance = this.end.getTime() - now.getTime();
        if (distance < 0) {
          //4th phase
          clearInterval(timer);
          return; //add animation
        }
        const hours = Math.floor(distance / this._hours);
        const minutes = Math.floor((distance % this._hours) / this._minutes);
        const seconds = Math.floor((distance % this._minutes) / this._seconds);
        this.displaySeconds = seconds < 10 ? "0" + seconds : seconds;
        this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
        this.displayHours = hours < 10 ? "0" + hours : hours;
        this.loaded = true;
      }, 1000);
    },
  },
};
</script>

<style lang="scss" scoped></style>
