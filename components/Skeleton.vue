<template>
  <div
    v-if="type === 'image' && imageUrl"
    class="focus:outline-none"
    :class="{
      'bg-gray-400 dark:bg-dark-600 bg-opacity-50 w-full animate-pulse bg-no-repeat':
        itemLoaded === false,
    }"
    :style="{
      backgroundImage: itemLoaded === true ? `url('${imageUrl}')` : '',
      backgroundPosition: 'center',
      backgroundSize: 'cover',
    }"
  >
    <img
      :src="imageUrl"
      class="invisible"
      draggable="false"
      alt="image"
      width="100%"
      height="100%"
      @load="itemLoaded = true"
    />
  </div>
</template>

<script>
export default {
  name: 'SkeletonLoader',
  props: {
    type: {
      type: String,
      required: false,
      default: 'block',
    },
    imageUrl: {
      type: String,
      required: false,
      default: null,
    },
    backgroundSize: {
      type: String,
      required: false,
      default: 'cover',
    },
    iframeUrl: {
      type: String,
      required: false,
      default: null,
    },
  },
  data() {
    return {
      itemLoaded: false,
    }
  },
}
</script>

<style></style>
