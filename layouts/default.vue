<template>
  <div>
    <Header />
    <Nuxt />
  </div>
</template>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.btn {
  @apply font-bold py-2 px-4 rounded;
}
.btn-teal {
  @apply bg-teal-500 text-white;
}
.btn-teal:hover {
  @apply bg-teal-700;
}
.btn-indigo {
  @apply bg-indigo-500 text-white;
}
.btn-indigo:hover {
  @apply bg-indigo-700;
}
</style>
