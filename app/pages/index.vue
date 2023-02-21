<template>
  <section class="home">
    <div class="mx-auto flex flex-wrap flex-col md:flex-row items-start">
      <div class="flex flex-col w-full xl:w-3/5 xl:pr-12 items-center justify-center relative">
        <h1 class="text-4xl md:text-6xl absolute text-white font-title">
          {{ welcomeHeadline }}
        </h1>
        <img
          :title="heroTitle"
          width="740"
          height="490"
          class="rounded shadow-xl w-full"
          :src="heroImg"
          :alt="heroAlt"
        />
      </div>
      <div class="flex flex-col w-full xl:w-2/5 justify-center lg:items-start overflow-y-hidden">
        <div
          v-html="$md.render(welcomeText + '\n\n --- \n\n' + welcomeTextFr)"
          class="home__welcome markdown"
        />
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';

@Component({
  // Called to know which transition to apply
  transition() {
    return 'slide-left';
  },
})
export default class Home extends Vue {
  [x: string]: any;

  welcomeHeadline = settings.welcomeHeadline;

  heroTitle = settings.heroTitle;

  heroImg = settings.heroImg;

  heroAlt = settings.heroAlt;

  welcomeText = settings.welcomeText;

  welcomeTextFr = settings.welcomeTextFr;

  get posts(): Post[] {
    return this.$store.state.posts;
  }
}
</script>
