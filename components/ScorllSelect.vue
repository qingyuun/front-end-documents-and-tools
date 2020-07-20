<template>
  <el-select
    v-scroll="handleScrollLoading"
    v-model="scorllSelectid"
    :remote-method="handleFilterRemote"
    :placeholder="placeholder"
    class="init_select"
    size="small"
    remote
    clearable
    filterable
  >
    <template v-if="$slots.prefix" slot="prefix">
      <slot name="prefix"/>
    </template>
    <el-option
      v-for="(item, index) in selectData"
      :key="index"
      :label="item.name"
      :value="item.id"
    />
  </el-select>
</template>

<script>
import { Select } from 'element-ui'
export default {
  name: 'ScrollSelect',
  props: {
    ...Select.props,
    request: {
      type: Function,
      required: true,
      default: () => {}
    },
    placeholder: {
      type: String,
      default: () => '请输入关键词'
    },
    value: {
      type: [String, Number],
      default: () => ''
    },
    customerNodeData: {
      type: Object,
      default: () => { return { name: '', id: null } }
    }
  },
  data() {
    return {
      scorllSelectid: null,
      scorllSelectloading: false,
      selectData: [],
      param: {
        name: '', // 关键字查询
        pageIndex: 1, // 分页中请求的页面
        pageCount: 5 // 自定义  每页的大小
      },
      pageLimit: 5, // 需维护数组的长度
      pageMap: [], // 对应数组长度的页码表
      totalCount: 0 // 数据总量
    }
  },
  watch: {
    value(val) {
      this.scorllSelectid = val
    },
    scorllSelectid(val) {
      this.$emit('change', val)
    },
    customerNodeData(val) {

    },
    selectData(val) {

    }
  },
  created() {
    this.postSelectList()
  },
  methods: {
    /**
     * select 滚动事件
     * @param param 滚动方向 true 下 false 上
     * @param el 当前DOM
     * @param middlePosition 滚动条位置
     */
    handleScrollLoading(param, el, middlePosition) {
      if (!this.scorllSelectloading) {
        if (param) {
          // 如果已是最后一页，则直接return
          if (this.totalCount <= this.param.pageIndex * this.param.pageCount) return
          ++this.param.pageIndex
          this.postSelectList(param, el, middlePosition)
        } else {
          // 如果在向上滚动时，如果还没有到达第一页则继续加载。 如果已到达则停止加载
          if (this.pageMap[0] > 1) this.param.pageIndex = this.pageMap[0] - 1
          else return false
          this.param.pageIndex = this.pageMap[0]
          --this.param.pageIndex
          this.postSelectList(param, el, middlePosition)
        }
      }
    },
    /**
    * 远程搜索
    * @param value 关键字
    */
    handleFilterRemote(value) {
      // 每次触发时页码初始化
      this.param.pageIndex = 1
      // 页码表也进行初始化
      this.pageMap = [1]
      this.param.name = value
      this.postSelectList()
    },
    /**
    * 请求数据方法
    * @param param 滚动方向
    * @param el 当前 DOM 元素
    * @param middlePosition 滚动条位置
    */
    postSelectList(param, el, middlePosition) {
      this.scorllSelectloading = true
      this.request(this.param).then(res => {
        this.totalCount = res.totalCount
        if (res) {
          if (this.value !== '') {
            /**
             * 自定义节点数据 位于绑定数据 位置索引
             * 循环绑定数据 循环数据 依次转换为字符串 并 和 自定义节点数据转换为字符串后比较 相等拿到当前索引
             * 判断索引 存在正确索引 对数据进行切割 去除 添加的自定义节点数据
             */
            let customreNodeDataIndex = null
            this.selectData.forEach((item, index) => { item.toString() === this.customerNodeData.toString() ? customreNodeDataIndex = index : null })
            customreNodeDataIndex ? this.selectData.splice(customreNodeDataIndex, 1) : null
            /**
             * 自定义节点数据 位于请求数据 位置索引
             * 循环请求数据 循环数据 对比id 判断是都存在 为this.value 的数据 存在拿到当前索引
             * 判断索引 存在不进行任何操作 不存在 将自定义数据 添加至请求数据中
             */
            let resindex = null
            res.items.forEach((item, index) => { item.id === this.value ? resindex = index : null })
            console.log(this.customerNodeData)
            resindex ? null : res.items.push(this.customerNodeData)
          }

          // 总页面统计，向上取整
          if (param === true) {
            // 向下滚动则尾部追究数据
            if (this.pageMap.length >= this.pageLimit) {
              // 当长度相等的时候， 绝对不能超出长度  则有进必有出
              // 删除 pageMap 列表的第一个元素
              this.pageMap.shift()
              // 对应删除页面的数据长度
              this.selectData.splice(0, this.param.pageCount)
              el.scrollTop = middlePosition
            }
            // 向尾部添加数据
            this.pageMap.push(this.param.pageIndex)
            this.selectData.push(...res.items)
          } else if (param === false) {
            this.pageMap = [this.param.pageIndex, ...this.pageMap]
            this.selectData = this.selectData.splice(-this.param.pageCount, this.param.pageCount)
            this.selectData = [...res.items, ...this.selectData]
            el.scrollTop = middlePosition
          } else {
            // 否则则是初始化加载，只有一页数据
            this.selectData = res.items
          }
          this.scorllSelectloading = false
        }
      }).catch(() => {
        this.scorllSelectloading = false
      })
    }
  }
}
</script>

<style lang='scss'>
  .customize_overflow{
    float: left;
    width:calc(100% - 260px);
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
</style>
