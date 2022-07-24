# 原作者
[GitHub-Laziji](https://github.com/GitHub-Laziji/menujs)

# 为什么升级
1. 修复vue2.7及以上版本不兼容问题
1. 修复超出边界展示问题

Vue 原生实现右键菜单组件, 零依赖


# 快速安装

## npm 安装
```
npm install h-vue-contextmenu
```
或
```
yarn add h-vue-contextmenu
```

## CDN
```html
<script src="https://unpkg.com/h-vue-contextmenu/dist/contextmenu.umd.js">
```


# 使用
CDN引入则不需要 `Vue.use(Contextmenu)`
> 测试中使用的是`element-ui`图标
```js
import Contextmenu from "h-vue-contextmenu"
Vue.use(Contextmenu);


// 在组件中调用显示菜单
// this.$contextmenu(options:MenuOptions);
// 鼠标点击或滚轮自动销毁, 也可手动销毁
// this.$contextmenu.destroy();

// 去除浏览器默认菜单
// event.preventDefault();
```


```html
<template>
  <div id="app" style="width:100vw;height:100vh" @contextmenu.prevent="onContextmenu"></div>
</template>

<script>
export default {
  methods: {
    onContextmenu(event) {
      this.$contextmenu({
        items: [
          {
            label: "返回(B)",
            onClick: () => {
              this.message = "返回(B)";
              console.log("返回(B)");
            }
          },
          { label: "前进(F)", disabled: true },
          { label: "重新加载(R)", divided: true, icon: "el-icon-refresh" },
          { label: "另存为(A)..." },
          { label: "打印(P)...", icon: "el-icon-printer" },
          { label: "投射(C)...", divided: true },
          {
            label: "使用网页翻译(T)",
            divided: true,
            minWidth: 0,
            children: [{ label: "翻译成简体中文" }, { label: "翻译成繁体中文" }]
          },
          {
            label: "截取网页(R)",
            minWidth: 0,
            children: [
              {
                label: "截取可视化区域",
                onClick: () => {
                  this.message = "截取可视化区域";
                  console.log("截取可视化区域");
                }
              },
              { label: "截取全屏" }
            ]
          },
          { label: "查看网页源代码(V)", icon: "el-icon-view" },
          { label: "检查(N)" }
        ],
        event,
        //x: event.clientX,
        //y: event.clientY,
        customClass: "class-a",
        zIndex: 3,
        minWidth: 230
      });
      return false;
    }
  }
};
</script>
```


# 参数说明

## MenuOptions

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
| :----: | :----: | :----: | :----: | :----: |
| items | 菜单结构信息 | `MenuItemOptions[]` | — | — |
| event | 鼠标事件信息 | `Event` | — | — |
| x | 菜单显示X坐标, 存在`event`则失效 | `number` | — | `0` |
| y | 菜单显示Y坐标, 存在`event`则失效 | `number` | — | `0` |
| zIndex | 菜单样式`z-index` | `number` | — | `2` |
| customClass | 自定义菜单class | `string` | — | — |
| minWidth | 主菜单最小宽度 | `number` | — | `150` |

## MenuItemOptions

| 属性 | 描述 | 类型 | 可选值 | 默认值 |
| :----: | :----: | :----: | :----: | :----: |
| label | 菜单项名称 | `string` | — | — |
| icon | 菜单项图标, 生成`<i class="icon"></i>`元素 | `string` | — | — |
| disabled | 是否禁用菜单项 | `boolean` | — | `false` |
| divided | 是否显示分割线 | `boolean` | — | `false` |
| customClass | 自定义子菜单class | `string` | — | — |
| minWidth | 子菜单最小宽度 | `number` | — | `150` |
| onClick | 菜单项点击事件 | `Function()` | — | — |
| children | 子菜单结构信息 | `MenuItemOptions[]` | — | — |
