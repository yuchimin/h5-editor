<template>
  <div class="container" v-if="attr">
    <el-row :gutter="10" v-if="attrShow.color">
      <el-col :span="6" class="label">字体色:</el-col>
      <el-col :span="18">
        <color-picker v-model="attr.color" />
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="attrShow.fontSize">
      <el-col :span="6" class="label">字号:</el-col>
      <el-col :span="18">
        <el-slider v-model="attr.fontSize" show-input size="small" />
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="attrShow.fontWeight">
      <el-col :span="6" class="label">粗细:</el-col>
      <el-col :span="18">
        <el-slider v-model="attr.fontWeight"
          size="small"
          :step="10"
          show-stops
          :max="90"
          :format-tooltip="formatWeight"
        />
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="attrShow.textAlign">
      <el-col :span="6" class="label">对齐:</el-col>
      <el-col :span="18" class="input-box">
        <radio-bar v-model="attr.textAlign" class="align-box">
          <radio-item label="left"><i class="iconfont icon-text-left" /></radio-item>
          <radio-item label="center"><i class="iconfont icon-text-center" /></radio-item>
          <radio-item label="right"><i class="iconfont icon-text-right" /></radio-item>
        </radio-bar>
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="attrShow.width" type="flex" align="middle">
      <el-col :span="6" class="label">宽高:</el-col>
      <el-col :span="18" class="input-box">
        <el-tooltip class="item" effect="dark" content="宽" placement="top-start">
          <el-input-number size="small" v-model="attr.width" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="高" placement="top-start">
          <el-input-number size="small" v-model="attr.height" />
        </el-tooltip>
      </el-col>
    </el-row>
    <el-row :gutter="10" v-if="attrShow.padding" type="flex" align="middle">
      <el-col :span="6" class="label">内边距:</el-col>
      <el-col :span="18" class="input-box">
        <el-tooltip class="item" effect="dark" content="上" placement="top-start">
          <el-input-number size="small" v-model="attr.padding[0]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="右" placement="top-start">
          <el-input-number size="small" v-model="attr.padding[1]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="下" placement="top-start">
          <el-input-number size="small" v-model="attr.padding[2]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="左" placement="top-start">
          <el-input-number size="small" v-model="attr.padding[3]" />
        </el-tooltip>
      </el-col>
    </el-row>
    <el-row :gutter="10" v-if="attrShow.margin" type="flex" align="middle">
      <el-col :span="6" class="label">外边距:</el-col>
      <el-col :span="18" class="input-box">
        <el-tooltip class="item" effect="dark" content="上" placement="top-start">
          <el-input-number size="small" v-model="attr.margin[0]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="右" placement="top-start">
          <el-input-number size="small" v-model="attr.margin[1]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="下" placement="top-start">
          <el-input-number size="small" v-model="attr.margin[2]" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="左" placement="top-start">
          <el-input-number size="small" v-model="attr.margin[3]" />
        </el-tooltip>
      </el-col>
    </el-row>
    <el-row :gutter="10" v-if="attrShow.background" type="flex" align="middle">
      <el-col :span="6" class="label">背景色:</el-col>
      <el-col :span="18">
        <color-picker v-model="attr.background" />
      </el-col>
    </el-row>
    <el-row :gutter="10" type="flex" align="middle" v-if="attrShow.borderRadius">
      <el-col :span="6" class="label">圆角:</el-col>
      <el-col :span="18" class="border-box">
        <el-input-number size="small" v-model="attr.borderRadius[0]" style="margin-right: 10px;"/>
        <el-radio-group v-model="attr.borderRadius[1]">
          <el-radio label="px" />
          <el-radio label="%" />
        </el-radio-group>
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="attrShow.border" type="flex" align="middle">
      <el-col :span="6" class="label">边框:</el-col>
      <el-col :span="18" class="border-box">
        <el-input-number size="small" v-model="attr.border[0]" />
        <color-picker
          style="margin: 0 10px;"
          v-model="attr.border[2]"
        />
        <el-select v-model="attr.border[1]" placeholder="请选择" size="small">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
      </el-col>
    </el-row>

    <el-row :gutter="10" type="flex" align="middle" v-if="attrShow.position">
      <el-col :span="6" class="label">绝对定位:</el-col>
      <el-col :span="18" class="input-box">
        <el-switch
          v-model="position"
          active-color="#FD7F6B"
          size="mini">
        </el-switch>
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="position" type="flex" align="middle">
      <el-col :span="6" class="label">定位:</el-col>
      <el-col :span="18" class="input-box">
        <el-tooltip class="item" effect="dark" content="上" placement="top-start">
          <el-input-number size="small" v-model="attr.top" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="右" placement="top-start">
          <el-input-number size="small" v-model="attr.right" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="下" placement="top-start">
          <el-input-number size="small" v-model="attr.bottom" />
        </el-tooltip>
        <el-tooltip class="item" effect="dark" content="左" placement="top-start">
          <el-input-number size="small" v-model="attr.left" />
        </el-tooltip>
      </el-col>
    </el-row>

    <el-row :gutter="10" v-if="position" type="flex" align="middle">
      <el-col :span="6" class="label">层级:</el-col>
      <el-col :span="18">
        <el-slider
          v-model="attr.zIndex"
          :step="100"
          :max="1000"
          show-stops>
        </el-slider>
      </el-col>
    </el-row>

  </div>
</template>

<script>
import { RadioBar, RadioItem } from '@/components/radio'
import ColorPicker from '@/components/ColorPicker'
import { toStyleString } from '@/utils/transformStyle'
const initMap = {
  color: '#000',
  fontSize: 16,
  fontWeight: 40,
  textAlign: 'left',
  width: undefined,
  height: undefined,
  margin: [0, 0, 0, 0],
  padding: [0, 0, 0, 0],
  border: [0, 'solid', '#000'],
  borderRadius: [0, 'px'],
  background: 'transparent',
  position: 'relative'
}
export default {
  name: 'Container',
  props: {
    attrData: Object,
    attrShow: Object
  },
  data () {
    return {
      attr: null,
      options: [{
        label: '---',
        value: 'dashed'
      }, {
        label: '——',
        value: 'solid'
      }],
      position: false
    }
  },
  mounted () {
    this.init()
  },
  watch: {
    attr: {
      handler () {
        this.$store.dispatch('updateStyle', toStyleString(this.attr))
      },
      deep: true
    },
    attrData () {
      this.init()
      if (this.attrData && this.attrData.position === 'absolute') {
        this.position = true
      } else {
        this.position = false
      }
    },
    position () {
      this.attr.position = this.position ? 'absolute' : 'relative'
      if (!this.position) {
        this.$delete(this.attr, 'left')
        this.$delete(this.attr, 'right')
        this.$delete(this.attr, 'bottom')
        this.$delete(this.attr, 'top')
        this.$delete(this.attr, 'zIndex')
      } else {
        this.attr = {left: undefined, top: undefined, right: undefined, bottom: undefined, zIndex: 0, ...this.attr}
      }
    }
  },
  components: {
    RadioBar, RadioItem, ColorPicker
  },
  methods: {
    formatWeight (val) {
      if (val === 40) {
        return 'normal'
      }
      if (val === 70) {
        return 'bold'
      }
      return val * 10
    },
    // 初始化样式值
    init () {
      const initMapCopy = JSON.parse(JSON.stringify(initMap))
      if (!this.attrShow) return
      let initData = {}
      for (let key in this.attrShow) {
        let item = {}
        item[key] = !this.attrData[key] ? initMapCopy[key] : this.attrData[key]
        initData = Object.assign(initData, item)
      }
      this.attr = initData
    }
  }
}
</script>

<style scoped lang="scss">
.label {
  margin-top: 4px;
}
.border-box {
  display: flex;
  align-items: center;
}
.input-box {
  margin-top: 6px;
}
</style>

<style lang="scss">
.std-radio-active i {
  color: $themeColor;
}
.el-radio + .el-radio {
  margin-left: 10px;
}
.el-radio__label {
  padding-left: 5px;
}
.el-radio__inner {
  width: 10px;
  height: 10px;
}
.container {
  .el-slider__runway.show-input {
    margin-right: 60px;
  }
  .el-slider__runway {
    margin: 10px 0;
    height: 4px;
  }
  .el-slider__bar {
    height: 4px;
  }
  .el-slider__button {
    width: 12px;
    height: 12px;
  }
  .el-slider__button-wrapper {
    top: -16px;
  }
  .el-slider__stop {
    width: 4px;
    height: 4px;
  }
}
</style>

