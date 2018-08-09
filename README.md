## React-loadList
  基于React实现的移动端三维度筛选条件组件

## 何时使用
筛选分类使用

## 代码演示

### 默认                        
```jsx
import React, { Component } from 'react';
import {  ScreeningClass, ScreeningContent } from './src/index';

const data = [
  'Racing car sprays burning fuel into crowd.',
  'Japanese princess to wed commoner.',
  'Australian walks 100km after outback crash.',
  'Man charged over missing wedding girl.',
  'Los Angeles battles huge wildfires.',
];

export default class Demo00 extends Component{
    handleChangeQuery(newState) {//筛选结果
        console.log('接收值',newState)
    }
    render() {
        return (
            <ScreeningClass 
                className = {className}
                onChange = {this.handleChangeQuery}
            >
                <ScreeningContent
                    order = '0'
                    tabName = {tagName}
                    content = { [{list:tagList, compareName: 'id', defaultValue:tag}] }
                />
                <ScreeningContent
                    order = '1'
                    tabName = {areaName}
                    content = {
                        [
                            {list:areaList, compareName: 'gbCode', defaultValue:defaultAreaCode},
                            {list:bizZoneList, compareName: 'id', defaultValue:mchtZoneid, nearValue:distance}
                        ]
                    } 
                />
                <ScreeningContent
                    order = '2'
                    tabName = {joinName}
                    content = { [{list:joinList, compareName: 'id', defaultValue:join}] }
                />                
            </ScreeningClass>
        )
    }
}
```

## 当前主要功能
- 获取综合筛选结果

## API
### ScreeningClass

| 参数 | 说明 | 类型 | 默认值 |
|---|---|---|---|
|className | 类名 | String | '' |
|onChange | 选择所有筛选后的回调事件，里面储存着此次调用的所有结果,return Array | Function | [] |

### ScreeningContent

| 参数 | 说明 | 类型 | 默认值 |
|---|---|---|---|
|order | 同onChange事件中的类id,用以区分当前获取不同的分类数据 | String | null |
|tabName | 标题名 | String | null |
|content | 当前分类有几级选择，最多两层，每一级选择对应的数据默认值等 | Array | null |
|content[i].list | 当前层级的list数据 | Array | null |
|content[i].compareName | 当前层级的关键值比对值名 | String | null |
|content[i].defaultValue | 当前层级的默认值名 | String | null |

## 最终拿到的集合
```js
[{
    id: 0, //类id
    tabName: //标题名
        tabKey: //标题值
        tabContent: [{
            level: 1,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }, {
            level: 2,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }]
}, {
    id: 1, //类id
    tabName: //标题名
        tabKey: //标题值
        tabContent: [{
            level: 1,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }, {
            level: 2,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }]
}, {
    id: 3, //类id
    tabName: //标题名
        tabKey: //标题值
        tabContent: [{
            level: 1,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }, {
            level: 2,
            levelData: {
                name: '全城',
                value: defaultTag, //值
                compareName: 'id', //关键值比对值名
            },
        }]
}]
```

