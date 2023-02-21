<template>
  <footer class="footer md:mx-0">
    <div class="container pb-12 flex min-w-full justify-center">
      <a
        href="https://facebook.com/AlliancefrancaisedeFionie"
        title="Link til Facebook-siden for Française Fyn"
      >
        <svg aria-hidden="true" width="32" height="32" viewBox="0 0 20 20" fill="black">
          <path
            d="M8.46 18h2.93v-7.3h2.45l.37-2.84h-2.82V6.04c0-.82.23-1.38 1.41-1.38h1.51V2.11c-.26-.03-1.15-.11-2.19-.11-2.18 0-3.66 1.33-3.66 3.76v2.1H6v2.84h2.46V18z"
            fill="black"
          ></path>
        </svg>
      </a>
    </div>
  </footer>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';

@Component
export default class Footer extends Vue {}
</script>

<style lang="scss">
.footer {
  background: linear-gradient(
    to right,
    #2184cd 0%,
    #2184cd 33%,
    white 33%,
    white 66%,
    red 66%,
    red 100%
  );
}
</style>
