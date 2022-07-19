<template>
  <div id="app">
    <Dialog :width="700" :title="title" :visible.sync='visible'
      @close='onClose'
      @open='onOpen'
    >
      <template #title>
        <div>slot title</div>
      </template>

      <template #default>
        <div>自定义内容</div>
      </template>
    </Dialog>
    <button @click='openDialog'>test</button>
  </div>
</template>

<script>
import Dialog from '@/components/DialogView.vue';

export default {
  name: 'App',
  data() {
    return {
      title: 'dialog title',
      visible: false,
    };
  },
  components: {
    Dialog,
  },
  methods: {
    onClose() {
      console.log('关闭事件');
    },
    onOpen() {
      console.log('打开事件');
    },
    openDialog() {
      this.visible = true;
    },
  },
};
</script>

<style>
 *{
    padding:0;
    margin:0;
 }
</style>
