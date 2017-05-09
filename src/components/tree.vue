<template>
  <li :class="{'expandable':tree.children,'last':tree.last}">
    <div class="hitarea" :class="{'open':isShow}" v-if="tree.children" @click.self="toggle(tree.children)"></div>
    <span :class="tree.children?'folder':'file'" :data="tree.value" @click.self="toggle(tree.children,tree.label,tree.value)">{{tree.label}}</span>
    <tree v-if="tree.children && isShow" :tree="item" :index.number="index" v-for="(item,index) in tree.children" :key="index"></tree>
  </li>
</template>

<script type="text/ecmascript-6">
  export default{
    name: 'tree',
    props: {
      tree: {
        type: Object,
        default: {}
      },
      index: {
        type: Number,
        default: 0
      },
      total: {
        type: Number,
        default: 0
      }
    },
    data () {
      return {
        isShow: false
      }
    },
    mounted () {
//      console.log(this.tree);
    },
    methods: {
      toggle (item, label, value) {
        if (item) {
          this.isShow = !this.isShow;
        } else {
          console.log('此处写最后一层的事件');
          console.log({label: label, value: value});
        }
      }
    }
  }
</script>

<style>
  .treeview, .treeview ul {
    padding: 0;
    margin: 0;
    list-style: none;
    background-color: white;
  }

  .treeview ul {
    margin-top: 3px;
  }

  .treeview .hitarea {
    background: url("../assets/tree/treeview-default.gif") -80px -3px no-repeat;
    height: 16px;
    width: 16px;
    margin-left: -16px;
    float: left;
    cursor: pointer;
  }

  .treeview .hitarea.open {
    background: url("../assets/tree/treeview-default.gif") -64px -25px no-repeat;
  }

  /* fix for IE6 */
  * html .hitarea {
    display: inline;
    float: none;
  }

  .treeview li {
    margin: 0;
    padding: 3px 0 3px 16px;
    text-align: left;
    text-indent: 2px;
    background: url("../assets/tree/treeview-default-line.gif") 0 0 no-repeat;
  }

  .treeview li.expandable {
    background-position: 0 -176px;
  }

  .treeview li.last {
    background-position: 0 -1766px
  }

  .filetree li {
    padding: 3px 0 2px 16px;
  }

  .filetree span.folder, .filetree span.file {
    padding: 1px 0 1px 16px;
    display: block;
    cursor: pointer;
  }

  .filetree li.expandable span.folder {
    background: url("../assets/tree/folder-closed.gif") 0 0 no-repeat;
  }

  .filetree li.expandable span.folder.open {
    background: url("../assets/tree/folder.gif") 0 0 no-repeat;
  }

  .filetree span.file {
    background: url("../assets/tree/file.gif") 0 0 no-repeat;
  }

</style>
