<template>
  <el-row type="flex" justify="center">
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 1, y: -1 })"
        :type="isActive({ x: 1, y: -1 })"
        icon="el-icon-top-left"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 1, y: 0 })"
        :type="isActive({ x: 1, y: 0 })"
        icon="el-icon-top"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 1, y: 1 })"
        :type="isActive({ x: 1, y: 1 })"
        icon="el-icon-top-right"
        circle
      ></el-button>
    </el-col>
  </el-row>
  <el-row type="flex" justify="center">
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 0, y: -1 })"
        :type="isActive({ x: 0, y: -1 })"
        icon="el-icon-back"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 0, y: 0 })"
        :type="isActive({ x: 0, y: 0 })"
        icon="el-icon-close"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: 0, y: 1 })"
        :type="isActive({ x: 0, y: 1 })"
        icon="el-icon-right"
        circle
      ></el-button>
    </el-col>
  </el-row>
  <el-row type="flex" justify="center">
    <el-col :span="2">
      <el-button
        @click="setActive({ x: -1, y: -1 })"
        :type="isActive({ x: -1, y: -1 })"
        icon="el-icon-bottom-left"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: -1, y: 0 })"
        :type="isActive({ x: -1, y: 0 })"
        icon="el-icon-bottom"
        circle
      ></el-button>
    </el-col>
    <el-col :span="2">
      <el-button
        @click="setActive({ x: -1, y: 1 })"
        :type="isActive({ x: -1, y: 1 })"
        icon="el-icon-bottom-right"
        circle
      ></el-button>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'ControlButtons',
  data() {
    return {
      activeButton: {
        x: 0,
        y: 0,
      },
    }
  },
  methods: {
    setActive(pos) {
      this.activeButton = pos
    },
    isActive(pos) {
      console.log(this.activeButton)
      return pos.x === this.activeButton.x && pos.y === this.activeButton.y ? 'primary' : ''
    },
  },
}
</script>

<style></style>
