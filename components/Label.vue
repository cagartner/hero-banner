<template>
  <div class="label" :style="{left: getOffset('left'), top: getOffset('top')}" @click="showContent = true">
    <button class="button label__button" @blur="showContent = false" @focusin="showContent = true" @keyup.space="showContent = true">
      <span class="sr-only">Offer Tag</span>
      <TagIcon />
    </button>
    <transition name="fade">
      <div v-if="showContent" class="label__content" :class="openSide">
        <a class="button button-primary">Shop Now</a>
        <h3>{{ title }}</h3>
        <p>{{ subtitle }}</p>
        <hr>
        <a href="link">{{ linkTitle }} <ArrowRight /></a>
      </div>
    </transition>
  </div>
</template>

<script>
import ArrowRight from "./icons/ArrowRight";
import TagIcon from "./icons/TagIcon";

export default {
  name: "Label",
  components: {TagIcon, ArrowRight},
  props: ['title', 'subtitle', 'link', 'linkTitle', 'offset', 'isMobile', 'openSide'],
  data() {
    return {
      showContent: false
    }
  },
  methods: {
    getOffset(position) {
      if (this.isMobile) {
        return this.offset.m[position] + 'px';
      }
      return this.offset.d[position] + 'px';
    }
  }
}
</script>
