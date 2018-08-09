## React-loadList
  基于React实现的移动端列表加载组件

## 何时使用
加载数据列表

## 代码演示

### 示例1--基本用法                        
```jsx
import React, { Component } from 'react';
import { LoadList } from '../src/index';

const data = [
  'Racing car sprays burning fuel into crowd.',
  'Japanese princess to wed commoner.',
  'Australian walks 100km after outback crash.',
  'Man charged over missing wedding girl.',
  'Los Angeles battles huge wildfires.',
];

export default class Demo00 extends Component{
    render(){
        return (
            <LoadList
                dataSource = {data}
                renderItem = {item =>(<div>{item}</div>)}
            />
        )
    }
}
```

### 示例2--获取后端返回的数据       
```jsx
import React, { Component } from 'react';
import { LoadListGetData } from '../src/index';

export default function Demo01(){        
    const queryParam = {
        pageSize:10,
        pageNo:1
    }
    return (
        <LoadListGetData
            queryParam = {queryParam}
            getData = {(queryParam) => new Promise(function(resolve, reject) {          
                    const postList = fetch('https://www.ucardvip.com/gateway/api/discount/getNearMchtShop', {method:'POST',body:JSON.stringify(queryParam)});
                    postList.then(result =>{
                        resolve({
                            code:result.code,
                            dataList:result.data.shopls,
                            errMsg:result.errMsg || '',
                        });
                    }).catch(function(error) {
                        reject(error);
                    });
                })
            }
            renderItem = {item =>(<div>{item.address}</div>)}
        />
    )
};
```

## 当前主要功能
- 解析后端返回的数据，可联合redux使用
- 自带获取数据中的加载中状态，获取数据后加载失效状态
- 可下滑刷新当前列表
- 下滑翻至下一页
- 翻到最后一页显示提示信息，默认“我是有底线的”

## API
### List

| 参数 | 说明 | 类型 | 默认值 |
|---|---|---|---|
|dataSource | 数据列表，常用redux的时候用 | Array | '' |
|getData | 与dataSoure API不能同时使用，返回的是promise，常用来使用AJAX或者fetch获取数据，常见用法见在示例2 | Promise | - |
|renderItem | 列表循环项,每个item能接收到的参数item, onChange, listIndex, array, itemKey | ReactNode | '' |
|stopFlip | 值为true时，禁止翻页 | boolean | false |
|isRefresh | 下滑刷新列表 | boolean | false |
|className | 列表样式 | string | load-list |
|renderDataIsNull | 数据返回为空时显示的组件，值为null时，显示默认组件 | ReactNode/null | null |
|renderPageEnd | 访问到最后一页时显示的组件，值为null时，显示默认组件 | ReactNode/null | null |
|renderServiceError | 服务器返回错误时时显示的组件，值为null时，显示默认组件 | ReactNode/null | null |
|onServiceError | 服务器返回的错误时，处理的信息，如会话过期，操作失败，系统错误等错误发生后，希望调用的事件 | function/null | null |

