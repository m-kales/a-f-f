<template>
  <article v-if="post" class="post" :class="post.slug">
    <div class="py-8 md:py-16 text-center w-11/12 md:w-5/6 xl:w-6/12 mx-auto">
      <nuxt-link to="/blog" class="flex mb-8">
        <svg
          class="w-5 mr-1"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fillRule="evenodd"
            d="M18 10a.75.75 0 01-.75.75H4.66l2.1 1.95a.75.75 0 11-1.02 1.1l-3.5-3.25a.75.75 0 010-1.1l3.5-3.25a.75.75 0 111.02 1.1l-2.1 1.95h12.59A.75.75 0 0118 10z"
            clipRule="evenodd"
          />
        </svg>
        Tilbage
      </nuxt-link>
      <h1 class="text-4xl xl:text-5xl font-title">
        {{ post.title }}
      </h1>
    </div>

    <div
      v-html="$md.render(post.content)"
      class="post__content markdown md:pb-24 w-11/12 md:w-5/6 xl:w-6/12 mx-auto"
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
      const post = await require(`@/content/blog/${params.slug}.json`);

      return {
        post,
      };
    } catch (e) {
      throw new Error('Not found');
    }
  }
}
</script>
