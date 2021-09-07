<template>
  <div class="label" :style="{left: getOffset('left'), top: getOffset('top')}" @click="showContent = true">
    <button class="button label__button" @blur="showContent = false" @focusin="showContent = true" @keyup.space="showContent = true">
      <span class="sr-only">Offer Tag</span>
      <TagIcon />
    </button>
    <transition name="fade">
      <div v-if="showContent" class="label__content" :class="openSide">
        <a class="button button-primary" target="_blank" :href="link" title="Shop Now">Shop Now</a>
        <h3>{{ title }}</h3>
        <p>{{ subtitle }}</p>
        <hr>
        <a :href="shopAllLink" target="_blank" :title="linkTitle">{{ linkTitle }} <ArrowRight /></a>
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
  props: {
    title: {
      type: String,
      default: null
    },
    subtitle: {
      type: String,
      default: null
    },
    link: {
      type: String,
      default: null
    },
    shopAllLink: {
      type: String,
      default: null
    },
    linkTitle: {
      type: String,
      default: null
    },
    openSide: {
      type: String,
      default: null
    },
    offset: {
      type: Object,
      default() {
        return {
          m: {
            top: 355,
            left: 500,
          },
          d: {
            top: 536,
            left: 900,
          }
        }
      }
    },
    isMobile: Boolean
  },
  data() {
    return {
      showContent: false
    }
  },
  created() {
    this.$nuxt.$on('hide-all-tags', () => {
      this.showContent = false;
    });
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
