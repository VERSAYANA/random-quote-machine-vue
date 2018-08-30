<template>
  <transition name="fade">
    <section v-show="!fetching" v-bind:class="{ fetching: fetching }">
      <p>{{ text }}</p>
      <span>{{ author }}</span>
      <div>
        <a target="_blank" v-bind:href="tweet">
          <svg viewBox="0 0 24 24">
            <path d="M22.46,6C21.69,6.35 20.86,6.58 20,6.69C20.88,6.16 21.56,5.32 21.88,4.31C21.05,4.81 20.13,5.16 19.16,5.36C18.37,4.5 17.26,4 16,4C13.65,4 11.73,5.92 11.73,8.29C11.73,8.63 11.77,8.96 11.84,9.27C8.28,9.09 5.11,7.38 3,4.79C2.63,5.42 2.42,6.16 2.42,6.94C2.42,8.43 3.17,9.75 4.33,10.5C3.62,10.5 2.96,10.3 2.38,10C2.38,10 2.38,10 2.38,10.03C2.38,12.11 3.86,13.85 5.82,14.24C5.46,14.34 5.08,14.39 4.69,14.39C4.42,14.39 4.15,14.36 3.89,14.31C4.43,16 6,17.26 7.89,17.29C6.43,18.45 4.58,19.13 2.56,19.13C2.22,19.13 1.88,19.11 1.54,19.07C3.44,20.29 5.7,21 8.12,21C16,21 20.33,14.46 20.33,8.79C20.33,8.6 20.33,8.42 20.32,8.23C21.16,7.63 21.88,6.87 22.46,6Z" />
          </svg>
        </a>
        <button v-on:click="next">Next</button>
      </div>
    </section>
  </transition>
</template>

<script lang="ts">
import Vue from 'vue';
import { setTimeout } from 'timers';

export default Vue.extend({
  name: 'HelloWorld',
  props: {
    text: String,
    author: String,
    fetching: Boolean,
    next: Function,
  },
  computed: {
    tweet(): string {
      return `https://twitter.com/intent/tweet?hashtags=quotes,simpsons&text="${
        this.text
      }%0A-${this.author}"`;
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
section {
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  padding: 32px 40px;
  width: 640px;
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background-color: #263238;
  color: var(--color-white);
  box-shadow: 0 8px 10px 1px rgba(0, 0, 0, 0.14),
    0 3px 14px 2px rgba(0, 0, 0, 0.12), 0 5px 5px -3px rgba(0, 0, 0, 0.4);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
p {
  font-size: 24px;
  margin: 24px 0;
}
span {
  align-self: flex-end;
  margin: 16px 0;
  font-size: 16px;
}
span:hover {
  color: var(--accent-color);
}
div {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
svg {
  width: 32px;
  height: 32px;
  fill: var(--color-white);
}
svg:hover {
  fill: var(--accent-color);
}
button {
  font-size: 14px;
  margin: 16px 0;
  border: 1px solid var(--color-white);
  box-sizing: border-box;
  height: 32px;
  width: 64px;
  background-color: transparent;
  color: var(--color-white);
  cursor: pointer;
  border-radius: 2px;
  outline: none;
}
button:hover {
  border-color: var(--accent-color);
  color: var(--accent-color);
}
@media (max-width: 768px) {
  section {
    width: 600px;
    padding: 16px 24px;
  }
  p {
    font-size: 20px;
  }
}
</style>
