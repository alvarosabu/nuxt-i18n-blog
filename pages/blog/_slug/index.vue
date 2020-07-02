<template>
  <div class="container mx-auto pt-6">
    <article v-if="post">
      <header class="grid grid-cols-2 gap-4 mb-12 rounded shadow-lg p-4">
        <img :src="post.media" alt="post.title" />
        <div class="">
          <h2 class="text-lg font-bold text-gray-800 mb-2">{{ post.title }}</h2>
          <p class="text-sm text-gray-700 mb-2">
            {{ $t('published-at') }} {{ getDate }}
          </p>
          <p class="text-sm text-gray-700">
            {{ $t('also-available-in') }}
            <nuxt-link
              class="uppercase text-teal-600 hover:text-teal-800"
              v-for="lang in otherLanguages"
              :key="lang.locale"
              :to="lang.path"
            >
              {{ lang.locale }}
            </nuxt-link>
          </p>
        </div>
      </header>
      <nuxt-content class="text-gray-800" :document="post" />
    </article>
  </div>
</template>

<script>
import { format } from 'date-fns'

const head = function () {
  return {
    title: this.post.title,
    htmlAttrs: {
      lang: this.$i18n.locale,
    },
    meta: [
      {
        hid: 'og:description',
        property: 'og:description',
        content: this.post.description,
      },
      {
        property: 'og:title',
        hid: 'og:title',
        content: this.post.title,
      },
      {
        hid: 'og:image',
        property: 'og:image',
        content: this.post.media,
      },
    ],
  }
}

const computed = {
  getDate() {
    return format(new Date(this.post.createdAt), 'dd/MM')
  },
  otherLanguages() {
    return this.post.otherLanguages || []
  },
}

export default {
  name: 'post',
  head,
  computed,

  async asyncData(context) {
    const { $content, params, app, route, redirect } = context
    const slug = params.slug
    const post = await $content(`${app.i18n.locale}/blog`, slug).fetch()

    return {
      post,
    }
  },
}
</script>

<style lang="scss">
.nuxt-content {
  h1,
  h2,
  h3,
  h4 {
    position: relative;
    font-weight: 700;
    margin-bottom: 2rem;
  }

  h1 {
    font-size: 2rem;
  }

  h2 {
    font-size: 1.75rem;
  }

  h3 {
    font-size: 1.5rem;
  }

  h4 {
    font-size: 1.25rem;
  }

  ul {
    list-style: disc;
  }

  ul,
  ol {
    margin: 1rem 0;
    padding-left: 40px;
  }

  ul,
  ol > li:last-child {
    margin-bottom: 10px;
  }

  table {
    margin-bottom: 10px;
    border-collapse: collapse;
  }

  th,
  td {
    padding: 0.5rem;
  }

  p {
    margin-bottom: 1rem;

    img {
      display: block;
    }

    img + em {
      display: block;
      margin-top: 0.5rem;
      font-size: 12px;
    }
  }
}
</style>
