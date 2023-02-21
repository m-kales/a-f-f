<template>
  <header class="flex items-center py-4 md:py-8">
    <div class="header__logo w-2 pl-4">
      <nuxt-link to="/">
        <img :src="logo" alt="Logo" />
      </nuxt-link>
    </div>

    <nav class="nav ml-auto">
      <ul
        class="flex md:flex-row flex-col items-end lg:items-center sm:mt-4 sm:pt-4 md:mt-0 md:pt-0 md:mr-4 lg:mr-8"
      >
        <li class="block font-medium px-4 py-1 md:p-2 lg:px-4">
          <nuxt-link to="/blog">
            Blog
          </nuxt-link>
        </li>

        <li
          v-for="(page, index) in pages"
          :key="index"
          class="block font-medium px-4 py-1 md:p-2 lg:px-4"
        >
          <nuxt-link :to="`/${page.slug}`">{{ page.title }}</nuxt-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';

@Component
export default class Header extends Vue {
  get pages(): Page[] {
    return this.$store.state.pages;
  }

  logo = settings.logo;
}
</script>

<style lang="scss">
.header__logo {
  width: 8rem;
  height: auto;
}
.nav {
  ul li > a {
    &.nuxt-link-active {
      &::after {
        content: '';
        position: absolute;
        left: 0;
        bottom: 0;
        right: 0;
        height: 0.2em;
        top: 1.2em;
        width: inherit;
        background: linear-gradient(
          to right,
          #2184cd 0%,
          #2184cd 33%,
          white 33%,
          white 66%,
          red 66%,
          red 100%
        );
        transition: all 0.3s cubic-bezier(0.75, -0.31, 0.41, 1.32);
        transform: scale(1, 1);
      }
      &:hover::after {
        transform: scale(0.9, 3);
        transform-origin: top;
      }
      color: $alliance;
      @apply font-bold;
    }
  }
}
</style>
