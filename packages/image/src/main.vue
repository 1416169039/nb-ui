<template>
  <div
    class="nb-image"
    :class="[ circle ? 'nb-image--circle' : '']"
    style="width: 100px; height: 100px"
  >
    <img :src="src" alt="test" :style="imgStyle" class="nb-image__inner" @click="showPreview" />
    <image-viewer
      v-if="isShowPreviewList"
      :onClose="hidePreview"
      :previewList="previewList"
      :src="src"
    ></image-viewer>
  </div>
</template>

<script>
import ImageViewer from "./image-preview";
export default {
  name: "NbImage",
  components: { ImageViewer },
  props: {
    src: {
      type: String,
      default: ""
    },
    type: {
      type: String,
      default: "cover",
      validator: t => {
        const acceptTypes = ["fill", "contain", "cover", "none", "scale-down"];
        return acceptTypes.includes(t);
      }
    }, //图片适应方式
    circle: {
      type: Boolean,
      default: false
    },
    previewList: {
      type: Array,
      default: () => {
        return [];
      }
    }
  },
  computed: {
    imgStyle() {
      let style = {
        "object-fit": this.type
      };
      return style;
    }
  },
  data() {
    return {
      isShowPreviewList: false
    };
  },
  methods: {
    showPreview() {
      this.isShowPreviewList = true;
    },
    hidePreview() {
      this.isShowPreviewList = false;
    }
  }
};
</script>

<style lang="scss" src="../../../theme/image.scss">
</style>