<template>
  <div class="space">
    <h1>盘古之白</h1>
    <div class="pangu-split" ref="splitElement">
      <Split v-model="split">
        <div slot="left" class="pangu-split-pane">
          <Input
            v-model="input"
            type="textarea"
            class="textarea-input"
            :autosize="{minRows: minRows, maxRows: maxRows}"
            show-word-limit
            placeholder="请输入内容"
          />
        </div>
        <div slot="right" class="pangu-split-pane">
          <Input
            v-model="output"
            class="textarea-input"
            type="textarea"
            :autosize="{minRows: minRows, maxRows: maxRows}"
            show-word-limit
            readonly
            style="padding-left: 5px; padding-right: 0px;"
          />
        </div>
      </Split>
    </div>
  </div>
</template>

<script>
  const pangu = require('pangu')

  export default {
    name: 'landing-page',
    data () {
      return {
        split: 0.5,
        minRows: 50,
        maxRows: 50,
        title: '空格处理',
        input: null,
        output: null
      }
    },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      }
    },
    watch: {
      input () {
        this.output = pangu.spacing(this.input)
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { font-family: 'Source Sans Pro', sans-serif; }

  .pangu-split {
    height: 1080px;
    margin: 0 10px 10px 10px;
    border: 1px solid #dcdee2;
  }

  .pangu-split-pane {
    padding: 10px;
  }

  .ivu-split-trigger-bar-con.vertical {
    display: none;
  }

  .ivu-split-pane, .ivu-split-pane.left-pane, .ivu-split-pane.right-pane {
    height: 1080px;
  }
</style>
