<script lang="ts" setup>
const props = defineProps({
  size: {
    type: String,
    default: 'base'
  },
})
</script>
<template>
<div class="slidev-layout section w-full h-full grid">
  <div class="my-auto prose h-full min-w-full flex flex-col px-10  justify-center" :class="[`prose-${size}`]">
    <slot />
  </div>
</div>
</template>
<style>
.slidev-layout {
  --tw-bg-opacity: 1;
  background-color: rgba(17,24,39,var(--tw-bg-opacity));
  background-image: none;
  color: rgba(243,244,246,var(--tw-text-opacity));
}
.prose .slidev-code-wrapper {
  display: flex;
  padding: 1rem  !important;
  background: linear-gradient(45deg,#11998e05,#23e75e05);
  justify-content: center;
  border-radius: 0.35rem !important;
  margin-bottom: 1rem !important;
}
.prose pre.shiki-container {
  font-family: 'Source Code Pro', monospace !important;
  margin: 0 !important;
  padding: 0 !important;
  display: inline-flex;
  justify-self: center;
  align-self: center;
}
.prose .slidev-code-wrapper > .shiki-container {
  margin-bottom: 0 !important;
}
.prose .shiki-dark {
  background-color: #101010 !important
}
h1 {
  background: linear-gradient(45deg,#11998e,#23e75e);
  font-weight: 700;
  margin-bottom: 0.5em;
  -webkit-background-clip: text!important;
  -webkit-text-fill-color: transparent!important;
}
.prose h1 {
  margin-bottom: 0.5em !important;
}
.prose li {
  list-style: none;
}
.prose li svg {
  margin: 0 !important;
}
</style>
