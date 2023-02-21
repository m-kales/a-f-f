<template>
  <article class="post" :class="post.slug">
    <div class="py-8 md:py-16 text-center mx-auto">
      <h1 class="text-4xl xl:text-5xl font-title">
        {{ post.title }}
      </h1>
    </div>

    <div
      v-html="$md.render(post.content)"
      class="post__content markdown pt-4 md:pt-6 md:pb-24 w-11/12 md:w-5/6 xl:w-6/12 mx-auto"
    />
  </article>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import { MetaInfo } from 'vue-meta';

@Component({
  head(): MetaInfo {
    return {
      title: this.post.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.post.seoDescription,
        },
        {
          hid: 'og:image',
          name: 'og:image',
          content: this.post.seoMetaImage,
        },
      ],
    };
  },
})
export default class BlogPost extends Vue {
  post!: Post;

  async asyncData({ params, payload }): Promise<{ post: Post }> {
    if (payload) {
      return { post: payload };
    }

    try {
      const post = require(`@/content/blog/${params.slug}.json`);

      return {
        post,
      };
    } catch (e) {
      throw new Error('Not found');
    }
  }
}
</script>
