![](./images/prettier.png)

## prettier使用

> 前端团队内日常开发中会面临多人修改同一个文件的问题，每个人都有自己的开发习惯，有人用Vscode，有人用Webstorm。而且每个人格式化代码的风格都不一致，导致后续再查看修改记录时，会很难追踪问题

### 安装
```bash
npm i prettier --save -dev
```
### 配置
#### 项目配置
1. 新建`.prettierrc.json`文件
```json
{
  "semi": true,  代码是否以;结尾
  "singleQuote": true, 是否使用单引号
  "printWidth": 120 每行最大的字符数换行
}
```
2. 新建`.prettierignore`文件，我们可能希望不自动格式化某个文件，可以将文件放在这个里面
```
src/components/clickOut.vue
```
3. 除了上述方法，我们也可以通过注释来让其忽略格式化文件或方法
```js
// prettier-ignore
export default {
  login          : () => import("@/pages/login/index.vue"),
  saleOrderDetail: () => import("@/pages/saleOrderDetail/index.vue")
}
```
4. 现在我们可以通过快捷键来格式化代码了，如果我们是在项目中期才引入Prettier的话，我们希望能批量的将制定目录下的文件都执行一次，就需要使用命令行工具了，我们可以通过`package.json`来配置
```json
"scripts": {
    ...
    "prettier": "prettier --write \"src/!(assets)/**/*.{js,ts,vue}\""
  },
```
通过配置我们能直接通过`yarn prettier`来执行命令(前提必须项目安装了prettier), 通过该命令，prettier会帮助我们将src下除assets文件夹外，所有的js,ts,vue文件
5. 如果我们希望能通过githook来强制提交时进行prettier,我们可以继续在package.json进行配置
```json
/* 前提安装了lint-staged包 */
"gitHooks": {
  "pre-commit": "lint-staged"
},
"lint-staged": {
  "*.{js,ts,vue}": [
    "prettier --write",
    "git add"
  ]
}
```
这样，每当我们通过git提交我们修改的代码时，prettier会帮助我们将提交的代码文件自动进行格式化

#### 编辑器配置
以Vscode为例，我们可以创建`.vscode`文件夹来保存项目的配置
```json
// .vscode > settings.json
{
  // Use the project's typescript version
  "typescript.tsdk": "node_modules/typescript/lib",
  "editor.formatOnSave": true,

  // Use prettier to format typescript, javascript and JSON files
  "[vue]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```
这样我们每次保存时，prettier会自动帮助我们对该文件进行格式化，免去了手动按快捷键的操作，至此Prettier简单的应用就完成了，从上面我们可以看到我们仅配置了一点设置，并没有大篇幅的设置很多，这就是Perttier同Spring Boot一样，是Opinionated的，无需过多配置

#### webstorm中如何进行prettier, 
1. 首先我们需要在插件中心安装Perttier插件，
2. 然后在Perttier的配置选项中，选择node_modules下安装的Perttier模块，或者直接选择全局安装的Perttier模块，即可通过快捷键进行格式化
3. 如果希望实现保存就自动格式化，需要通过file watch来实现该功能
