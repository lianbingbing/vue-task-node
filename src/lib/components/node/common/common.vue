<template>
<node :node="node" width=200 height=30 v-on:on-select="selectNodeMethod" v-on:on-drag-ging="dragGing" v-on:on-drag-start="dragStart" v-on:on-drag-end="dragEnd" v-on:updateTem="updateTemp" v-on:on-mouse="mouseMenu">
  <div :class="classes">
    <span :class="iconCls +' '+ [node.icon ? node.icon : 'task-icon-53']"></span>
    <span :class="nameCls">{{node.name}}</span>
    <span :class="statusCls +' '+ stateCls(node.state)"></span>
    <in-common-ls :in_ports="node.inPorts" v-on:on-add-path='addPath'></in-common-ls>
    <out-common-ls :out_ports="node.outPorts"></out-common-ls>
  </div>
</node>
</template>
<script>
import Node from '../node.vue'
import InPort from '../../port/inport.vue'
import OutPort from '../../port/outport.vue'
import InCommonLs from './incommonls.vue'
import OutCommonLs from './outcommonls.vue'
import mixinsNode from '../../../mixins/node'

const prefixCls = 'task-common-node'
export default {
  components: {
    OutCommonLs,
    InCommonLs,
    OutPort,
    InPort,
    Node},
  mixins: [ mixinsNode ],
  name: 'CommonNode',
  data () {
    return {
      state: ''
    }
  },
  props: {
    node: {
      id: [String, Number],
      name: {
        type: [String, Number],
        default: '节点'
      },
      positionX: {
        type: [String, Number],
        default: 0
      },
      positionY: {
        type: [String, Number],
        default: 0
      },
      icon: [String, Number],
      state: {
        type: [String, Number],
        default: 1
      },
      inPorts: {
        type: Array,
        default: []
      },
      outPorts: {
        type: Array,
        default: []
      }
    }
  },
  computed: {
    classes () {
      return [
        `${prefixCls}`
      ]
    },
    iconCls () {
      return [
        `${prefixCls}-icon`
      ]
    },
    nameCls () {
      return [
        `${prefixCls}-name`
      ]
    },
    statusCls () {
      return [
        `${prefixCls}-status`
      ]
    },
    selectedCls () {
      return [
        `task-node-selected`
      ]
    }
  },
  methods: {
    stateCls (value) {
      switch (value) {
        case 1: //等待中
          return "icon task-node-waiting state-await-color";
        case 2: //运行中
          return "icon task-node-running state-running-color";
        case 3: //已中止
          return "icon task-node-pause state-pause-color";
        case 4: //成功
          return "icon task-node-success state-success-color";
        case 5: //失败
          return "icon task-node-failed state-failed-color";
        default:
          //未运行
          return "icon task-node-waiting state-await-color";
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.state-success-color {
  color: #67c23a;
}
.state-failed-color {
  color: #f56c6c;
}
.state-pause-color {
  color: #e6a23c;
}
.state-running-color {
  color: #2b7bbb;
}
.state-await-color {
  color: #909399;
}
</style>