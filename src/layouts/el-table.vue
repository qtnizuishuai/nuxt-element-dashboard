<template>
  <div class="container">
    <el-data-table v-bind="$data"></el-data-table>
  </div>
</template>

<script>
import {formatDate} from '~/const/filter.js'
export default {
  name: 'el-table',
  data() {
    return {
      url: 'https://easy-mock.com/mock/5b586c9dfce1393a862d034d/example/img',
      // full attributes of columns see: http://element.eleme.io/#/zh-CN/component/table#table-column-attributes
      tableAttrs: {
        'cell-class-name': ({row, column, rowIndex, columnIndex}) => {
          if (rowIndex === 0 && columnIndex === 6) {
            return 'green'
          }
        }
      },
      columns: [
        // type: 'selection' will show checkbox
        // see http://element.eleme.io/#/zh-CN/component/table#table-column-attributes
        {type: 'selection', selectable: (row, index) => index > 0},
        {prop: 'code', label: '组件名称'},
        {prop: 'name', label: '分类'},
        {prop: 'alias', label: '版本'},
        {
          prop: 'logoUrl',
          label: '开发语言',
          width: '150px'
        },
        {
          prop: 'updatedAt',
          label: '最后更新时间',
          formatter: row => formatDate(row.updatedAt, 'YYYY-MM-DD'),
          width: '150px'
        },
        {
          prop: 'status',
          label: '状态',
          formatter: row => (row.status === 'normal' ? '上架' : '下架')
        }
      ],
      searchForm: [
        {
          $el: {placeholder: '请输入'},
          label: '组件名称',
          $id: 'code',
          $type: 'input'
        },
        {
          $el: {placeholder: '请输入'},
          label: '分类',
          $id: 'name',
          $type: 'input'
        },
        {
          $el: {placeholder: '请输入'},
          label: '状态',
          $id: 'status',
          $type: 'input'
        }
      ],
      form: [
        {
          $type: 'select',
          $id: 'backendFramework',
          label: '后端框架',
          rules: [{required: true, message: '请选择后端框架', trigger: 'blur'}],
          $options: ['DUBBO', 'HSF'].map(f => ({label: f, value: f})),
          $el: {
            placeholder: '请选择'
          }
        },
        {
          $type: 'input',
          $id: 'name',
          label: '名称',
          rules: [
            {
              required: true,
              message: '请输入名称',
              trigger: 'blur',
              transform: v => v && v.trim()
            }
          ],
          $el: {placeholder: '请输入'}
        }
      ],
      extraButtons: [
        {
          type: 'primary',
          text: '查看',
          atClick: row => {
            return new Promise((resolve, reject) => setTimeout(resolve, 1500))
          }
        },
        {
          text: '编辑',
          atClick: row => {
            return new Promise((resolve, reject) => setTimeout(resolve, 1500))
          }
        },
        {
          text: '下架',
          atClick: row => {
            return new Promise((resolve, reject) => reject())
          }
        }
      ],
      //  headerButtons: [
      //     {
      //     text: '自定义头部按钮',
      //     disabled: selected => selected.length == 0,
      //     atClick: selected => {
      //         let ids = selected.map(s => s.id)
      //         alert('selected ids: ' + ids)
      //         return new Promise((resolve, reject) => setTimeout(resolve, 1500))
      //     }
      //     },
      //     {
      //     text: '请求后不刷新',
      //     atClick: selected => {
      //         return new Promise((resolve, reject) =>
      //         setTimeout(() => resolve(false), 1500)
      //         )
      //     }
      //     }
      // ],
      hasEdit: false
      // hasNew: false,
      // hasDelete: false
    }
  },
  methods: {}
}
</script>
<style lang="stylus">
.container {
  padding: 20px 40px;

  .green {
    color: #cbe0b9;
  }
}
</style>
