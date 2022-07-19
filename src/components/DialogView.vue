<template>
    <div class='container' v-show='visible' @click.self='close'>
        <div class='main-container' :style='{ width : `${width}px` }' ref='container'>
            <div class='close'>
                <img src="@/assets/close.png" alt="" class='close-img' @click='close'>
            </div>
            <div class='title'>
                <!-- ? 优先slot -->
                <slot name='title' v-if='$slots.title'></slot>
                <div v-else>{{ title }}</div>
            </div>

            <!-- ? 自定义弹窗内容 -->
            <div class='content'>
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    // ? 自定义宽度
    width: {
      type: Number,
      default: 500,
    },
    // ? 自定义标题
    title: {
      type: String,
    },
    // ? 显示
    visible: {
      type: Boolean,
    },
  },
  methods: {
    close() {
      // ? 关闭
      this.$emit('update:visible', false);
    },
  },
  watch: {
    visible(newVal) {
      if (newVal) {
        this.$emit('open');
      } else {
        // ? 触发关闭事件
        this.$emit('close');
      }
    },
  },
};
</script>

<style scoped>
    .container{
        position: fixed;
        top:0;
        left:0;
        width: 100vw;
        height: 100vh;
        background-color: rgba(1, 1, 1, 0.4);
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 10;
    }

    .main-container{
        height: 400px;
        background-color: white;
        border-radius: 25px;
        display: flex;
        flex-direction: column;
        align-items: center;
        position: relative;
    }

    .close{
        position: absolute;
        right:-30px;
        top:0;
    }
    .close-img{
        width: 30px;
        height: 30px;
        cursor: pointer;
    }
</style>
