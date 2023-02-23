<template>
  <section class="page h-screen xl:w-1/2 mx-auto" :class="page.slug">
    <h1 class="page__title font-title text-4xl xl:text-5xl text-center py-8 md:py-16">
      {{ page.title }}
    </h1>
    <div
      v-html="$md.render(page.content)"
      class="page__content mx-auto markdown pt-4 md:pt-6 md:pb-24"
    />
    <div v-if="page.pdf">
      <ul class="font-title text-2xl underline">
        <li v-for="(pdfFile, index) in page.pdf" :key="index">
          <a :href="pdfFile.file" target="_blank">{{ pdfFile.title }}</a>
        </li>
      </ul>
    </div>
  </section>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import { MetaInfo } from 'vue-meta';

@Component({
  // Called to know which transition to apply
  transition(to, from) {
    if (!from) {
      return 'slide-left';
    }

    return 'slide-right';
  },

  head(): MetaInfo {
    return {
      title: this.page.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.page.seoDescription,
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: this.page.seoMetaImage,
        },
      ],
    };
  },
})
export default class PageTemplate extends Vue {
  page!: Page;

  async asyncData({ params, payload }): Promise<{ page: Page }> {
    if (payload) {
      return { page: payload };
    }

    try {
      const page = require(`@/content/pages/${params.page}.json`);

      return {
        page,
      };
    } catch (e) {
      throw new Error('Not found');
    }
  }
}
</script>
