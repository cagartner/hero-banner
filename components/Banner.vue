<template>
  <section class="hero-banner">
    <div class="hero-banner__content">
      <h1>the refresh sale</h1>
      <p>15% off sitewide to recharge your living space. Ends Friday, 2/19</p>
      <a href="#" class="button button-primary button-hero" tabindex="1">
        Start customizing
        <ArrowRight />
      </a>
    </div>

    <div ref="banner" class="hero-banner__image" @scroll="hideDragOption">
      <picture>
        <source media="(min-width:840px)" srcset="~/assets/images/banner-d.jpeg, ~/assets/images/banner-d-2x.jpg 2x, ~/assets/images/banner-d-3x.jpg 3x">
        <source srcset="~/assets/images/banner-m.jpeg, ~/assets/images/banner-m-2x.jpeg 2x, ~/assets/images/banner-m-3x.jpg 3x">
        <img ref="image" src="~/assets/images/banner-m.jpeg">
      </picture>

      <Label v-for="label in labels" :key="label.id"
             :title="label.title"
             :subtitle="label.subtitle"
             :link="label.link"
             :link-title="label.linkTitle"
             :offset="label.offset"
             :open-side="label.openSide"
             :is-mobile="isMobile" />

      <transition name="fade">
        <button v-if="showDragOption" class="button button-drag">
          <ArrowLeft />
          Drag to explore
          <ArrowRight />
        </button>
      </transition>
    </div>
  </section>
</template>

<script>
import ArrowRight from "./icons/ArrowRight";
import Label from "./Label";
import ArrowLeft from "./icons/ArrowLeft";

export default {
  name: "Banner",
  components: {ArrowLeft, Label, ArrowRight},
  data() {
    return {
      windowWidth: 0,
      imageWidth: 0,
      bannerOffSet: 0,
      showDragOption: false,
      labels: [
        {
          id: 1,
          title: 'Brooks Coffee Table',
          subtitle: 'White wash oak',
          link: '#',
          linkTitle: 'Shop all tables',
          openSide: 'right',
          offset: {
            m: {
              top: 365,
              left: 125,
            },
            d: {
              top: 453,
              left: 315,
            }
          }
        },
        {
          id: 2,
          title: 'Sloan Sectional',
          subtitle: 'Vintage Plush Pewter',
          link: '#',
          linkTitle: 'Shop all sectionals',
          openSide: 'left',
          offset: {
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
      ]
    }
  },
  computed: {
    isMobile() {
      return (this.windowWidth <= 840);
    }
  },
  mounted() {
    this.windowWidth = window.innerWidth;
    this.imageWidth = this.$refs.image.naturalWidth;

    if (this.windowWidth <= this.imageWidth) {
      this.setBannerOffset();
    }
  },
  methods: {
    setBannerOffset() {
      this.showDragOption = true;
    },

    hideDragOption() {
      this.showDragOption = false;
      this.$nuxt.$emit('hide-all-tags');
    },

    getImageOffset() {
      return this.imageWidth - this.windowWidth;
    }
  }
}
</script>
