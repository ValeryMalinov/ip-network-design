<template>
  <svg :x="x" :y="y">
    <rect
      :fill="color"
      stroke="#000000"
      :stroke-width="selected ? 2 : 0"
      x="5"
      y="12"
      rx="3"
      ry="3"
      :width="width"
      :height="height"
      class="node-dark-background"
    ></rect>
    <svg x="0" y="0" @mousedown="mouseDown" @mouseenter="mouseenter" @mouseleave="mouseleave">
      <rect
        fill="#000000"
        :fill-opacity="titleFillOpacity"
        x="7"
        y="14"
        rx="3"
        ry="3"
        :width="width-4"
        height="21"
        class="node-dark-background"
      ></rect>
      <text :x="10" :y="30" font-size="16" font-weight="bold" fill="#000000">{{title}}</text>
      <g v-if="deletable" @click="deleteNode">
        <rect
          :x="width - 12"
          y="18"
          width="14"
          height="14"
          rx="2"
          ry="2"
          fill="#ffffff"
          :fill-opacity="0.25"
        ></rect>
        <line
          :x1="width"
          :y1="20"
          :x2="width - 10"
          :y2="30"
          style="stroke:rgb(0,0,0);"
          stroke-width="2"
        ></line>
        <line
          :x1="width - 10"
          :y1="20"
          :x2="width"
          :y2="30"
          style="stroke:rgb(0,0,0);"
          stroke-width="2"
        ></line>
      </g>
    </svg>
    <rect
      fill="#ffffff"
      x="7"
      y="37"
      rx="3"
      ry="3"
      :width="width-4"
      :height="height - 27"
      class="node-light-background"
    ></rect>
    <slot></slot>
  </svg>
</template>
<script>
export default {
  name: "DiagramNode",
  props: {
    title: {
      type: String,
      required: true
    },
    index: Number,
    ports: {
      type: Array,
      default: () => {
        return [];
      }
    },
    x: Number,
    y: Number,
    width: {
      type: Number,
      default: 200
    },
    height: {
      type: Number,
      default: 250
    },
    color: {
      type: String,
      default: "#66cc00"
    },
    deletable: {
      type: Boolean,
      default: false
    },
    selected: Boolean
  },
  data() {
    return {
      nodeStrokeWidth: 0,
      titleFillOpacity: 0
    };
  },
  methods: {
    deleteNode: function() {
      this.$emit("delete");
    },
    mouseDown: function(event) {
      this.$emit(
        "onStartDrag",
        { type: "nodes", index: this.index, selected: this.true },
        event.x - this.x,
        event.y - this.y
      );
    },
    mouseenter() {
      this.titleFillOpacity = 0.35;
    },
    mouseleave() {
      this.titleFillOpacity = 0;
    }
  }
};
</script>