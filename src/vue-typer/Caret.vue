<template>
  <span class="caret custom" :class="animationClass"></span>
</template>

<script>
const ANIMATION_CLASS_PREFIX = "vue-typer-caret-";

export default {
  props: {
    /**
     *
     * Caret animation similar to Sublime and VSCode: 'solid', 'blink', 'smooth', 'phase', 'expand'.
     */
    animation: {
      type: String,
      default: "blink",
      validator: (value) =>
        /^solid$|^blink$|^smooth$|^phase$|^expand$/.test(value),
    },
  },
  computed: {
    animationClass() {
      return ANIMATION_CLASS_PREFIX + this.animation;
    },
  },
};
</script>

<style scoped lang="less">
@import "styles/typer-colors";
@import "styles/caret-animations";
span.caret {
  &:empty:before {
    content: "\200b"; // zero width space character
  }
}

/* Keep the following .caret styles as low-specificity as possible so they are more easily overridden */
span {
  display: inline-block;
  width: 1px;
}

.idle {
  background-color: @caret-idle-color;
}

.typing {
  background-color: @caret-typing-color;
}

.selecting {
  display: none;
  background-color: @caret-selecting-color;
}

.erasing {
  background-color: @caret-erasing-color;
}

.complete {
  display: none;
  background-color: @caret-complete-color;
}
</style>
