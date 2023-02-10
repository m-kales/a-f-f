<template>
  <main :class="[$route.name]" class="main px-4 md:px-0 font-sans">
    <div class="container mx-auto">
      <site-header />
      <nuxt class="nuxt" />
    </div>

    <svg class="divider" width="100%" viewBox="0 0 10 1">
      <defs>
        <linearGradient id="Gradient1">
          <stop offset="0%" stop-color="#2184cd" />
          <stop offset="33%" stop-color="#2184cd" />
          <stop offset="33%" stop-color="white" />
          <stop offset="66%" stop-color="white" />
          <stop offset="66%" stop-color="red" />
          <stop offset="100%" stop-color="red" />
        </linearGradient>
      </defs>

      <polygon
        class="polygon"
        stroke="none"
        fill="url(#Gradient1)"
        stroke-width="0"
        points="0,0.6
        0,1 10,1 10,0"
      />
    </svg>

    <site-footer />
  </main>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import SiteHeader from '@/components/partials/header.vue';
import SiteFooter from '@/components/partials/footer.vue';

@Component({
  components: {
    SiteHeader,
    SiteFooter,
  },
})
export default class DefaultLayout extends Vue {}
</script>

<style lang="scss">
.divider {
  position: relative;
  min-width: 100%;
  margin-top: auto;
}

.nuxt {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}
</style>
