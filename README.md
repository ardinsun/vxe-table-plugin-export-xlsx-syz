# vxe-table-plugin-export-xlsx-syz
基于 vxe-table 表格的扩展插件，支持导出 xlsx 格式


## Compatibility

此版本兼容vxe-table@4.0.0~4.5.9版本，并且支持导出xlsx格式。

使用场景：由于官方在4.5.10版本之后将setup方法调整为config（又在4.6.13将config换为setConfig），而vxe-table-plugin-export-xlsx没有兼容之前setup方式的版本。

导致在使用vxe-table@4.0.0~4.5.9版本并且鉴于不抗力无法升级版本的小伙伴没办法使用导出xlsx功能。


## Installing

```shell
npm install vxe-table vxe-table-plugin-export-xlsx-syz exceljs
```

```javascript
// ...
import { VxeUI } from 'vxe-table'
import VXETablePluginExportXLSXSyz from 'vxe-table-plugin-export-xlsx-syz'
import ExcelJS from 'exceljs'
// ...

// 方式1：NPM 安装，注入 ExcelJS 对象
VxeUI.use(VXETablePluginExportXLSXSyz, {
  ExcelJS
})

// 方式2：CDN 安装，只要确保 window.ExcelJS 存在即可
// VxeUI.use(VXETablePluginExportXLSXSyz)
```

## Demo

```html
<vxe-toolbar>
  <template v-slot:buttons>
    <vxe-button @click="exportEvent">导出.xlsx</vxe-button>
  </template>
</vxe-toolbar>

<vxe-table
  ref="xTable"
  height="600"
  :data="tableData">
  <vxe-column type="seq" width="60"></vxe-column>
  <vxe-column field="name" title="Name"></vxe-column>
  <vxe-column field="age" title="Age"></vxe-column>
  <vxe-column field="date" title="Date"></vxe-column>
</vxe-table>
```

```javascript
export default {
  data () {
    return {
      tableData: [
        { id: 100, name: 'test', age: 26, date: null },
        { id: 101, name: 'test1', age: 30, date: null },
        { id: 102, name: 'test2', age: 34, date: null }
      ]
    }
  },
  methods: {
    exportEvent() {
      this.$refs.xTable.exportData({
        filename: 'export',
        sheetName: 'Sheet1',
        type: 'xlsx'
      })
    }
  }
}
```