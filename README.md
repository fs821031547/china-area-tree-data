# 中国省市区树数据，中国省市区级联数据

## 安装

  `npm install china-area-tree-data -S`

## 使用

```js
import treeData from 'china-area-tree-data'
```

ant-design-vue 使用方式
```js
<template>
  <a-tree-select
    v-model="value"
    style="width: 100%"
    :tree-data="treeData"
    tree-checkable
    :show-checked-strategy="SHOW_PARENT"
    :replaceFields="{ title: 'label', key: 'value', value: 'value' }"
    search-placeholder="Please select"
  />
</template>
<script>
import treeData from 'china-area-tree-data'
const SHOW_PARENT = TreeSelect.SHOW_PARENT;
    export default {
    data() {
        return {
        value: ['0-0-0'],
        treeData,
        SHOW_PARENT,
        };
    },
    };
</script>   
```

## 数据结构示例

```js
export default [
    {
        'value': '310000',
        'label': '上海市',
        'children': [
            {
                'id': '1-5NWH',
                'value': '310100',
                'label': '上海市',
                'id': '1-5NWH',
                'children': [
                    {
                        'value': '310115',
                        'label': '浦东新区',
                    },
                    {
                        'value': '310117',
                        'label': '松江区',
                    }
                ]
            }
        ]
    },
    {
        'value': '530000',
        'label': '云南省',
        'children': [
            {
                'id': '1-5APO',
                'value': '530400',
                'label': '玉溪市',
                'children': [
                    {
                        'value': '530425',
                        'label': '易门县',
                    },
                    {
                        'value': '530428',
                        'label': '元江哈尼族彝族傣族自治县',
                    },
                ]
            }
        ]
    },
]
```

## 省市二级联动，只选择省市

```js
<template>
  <a-tree-select
    v-model="value"
    style="width: 100%"
    :tree-data="provinceCityData"
    tree-checkable
    :show-checked-strategy="SHOW_PARENT"
    :replaceFields="{ title: 'label', key: 'value', value: 'value' }"
    search-placeholder="Please select"
  />
</template>
<script>
    import treeData from 'china-area-tree-data'
    const provinceCityData = treeData
    // 过虑掉区域这一层级 遍历每个对象并删除第二层children
    provinceCityData.forEach(data => {
      if (data.children && data.children.length > 0) {
        data.children.forEach(child => {
          delete child.children
        })
      }
    })
    const SHOW_PARENT = TreeSelect.SHOW_PARENT;
    export default {
    data() {
        return {
        value: ['0-0-0'],
        provinceCityData,
        SHOW_PARENT,
        };
    },
    };
</script>   
```
