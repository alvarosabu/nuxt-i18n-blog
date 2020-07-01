<template>
  <header class="topnav h-54px p-2 border-b-2 border-gray-200">
    <div class="container mx-auto flex justify-between items-center">
      <div class="right flex justify-start items-center">
        <Logo class="w-8 h-8 mr-3" />
        <h1 class="text-lg font-bold text-gray-700">{{ title }}</h1>
      </div>
      <div class="left self-end" v-if="!isContentPage">
        <ul class="flex lang-switch justify-around">
          <li v-if="$i18n.locale !== 'en'">
            <nuxt-link
              class="text-md ml-3 font-semibold text-gray-600"
              :to="switchLocalePath('en')"
              >EN</nuxt-link
            >
          </li>
          <li v-if="$i18n.locale !== 'es'">
            <nuxt-link
              class="text-md ml-3 font-semibold text-gray-600"
              :to="switchLocalePath('es')"
              >ES</nuxt-link
            >
          </li>
          <li v-if="$i18n.locale !== 'fr'">
            <nuxt-link
              class="text-md ml-3 font-semibold text-gray-600"
              :to="switchLocalePath('fr')"
              >FR</nuxt-link
            >
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
const data = () => ({
  title: 'Nuxt-i18n Blog',
})

const computed = {
  isContentPage() {
    return this.$route.name.includes('slug')
  },
}

export default {
  name: 'Header',
  data,
  computed,
}
</script>

<style></style>
