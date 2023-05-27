<template>
  <div class="content-middle">
    <transition name="fade">
      <timer-component v-if="loaded"></timer-component>
    </transition>
    <transition name="fade">
      <waiting-component v-if="!loaded"></waiting-component>
    </transition>
  </div>
</template>

<script>
import TimerComponent from "@/components/TimerComponent.vue";
import WaitingComponent from "@/components/WaitingComponent.vue";
export default {
  components: { TimerComponent, WaitingComponent },
  name: "HomeView",
  data() {
    return {
      loaded: false,
    };
  },
  mounted() {
    setTimeout(() => {
      this.loaded = true;
    }, 1000);
  },
};
</script>
