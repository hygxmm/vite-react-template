# 从零到一建立一套完整的前端规范

## 代码规范之格式化规范

1. 安装依赖

```bash
npm install --save-dev --save-exact prettier
# or
yarn add --dev --exact prettier
```

2. 创建配置文件

```bash
echo {}> .prettierrc.json
```

3.

```bash
echo {}> .prettierignore

# 内容如下:
dist
build
coverage
```

4. 配置编辑器
   - 安装`Prettier-Code Formater`插件
   - 打开编辑器设置中的保存自定格式化代码(勾选 `format on save` 选项)
5. 安装`husky`和`lint-staged`插件

```bash
npm install --save-dev husky lint-staged
npx husky install
npm set-script prepare "husky install"
npx husky add .husky/pre-commit "npx lint-staged"
# or
yarn add --dev husky lint-staged
npx husky install
npm set-script prepare "husky install"
npx husky add .husky/pre-commit "npx lint-staged"
```

6. 将一下内容添加到`package.json`中

```json
{
  "lint-staged": {
    "**/*": "prettier --write --ignore-unknown"
  }
}
```

7. 若使用的是脚手架工具搭建的项目，会自带 eslint 配置（eslintConfig）。prettier 和 eslint 会有一些配置上的冲突，这个时候需要安装`eslint-config-prettier`以使`ESLint`和`Prettier`相互配合，安装完后在`.eslintrc`中配置,这样就可以用`prettier`的部分规则覆盖前面的规则，让它们都能正常工作。

```json
"eslintConfig": {
    "extends": [
        "react-app",
        "react-app/jest",
        "prettier"
    ]
}
```

## 代码规范之 JS/TS 规范

1. 安装依赖

```bash
npm install eslint --save-dev
# or
yarn add eslint --dev
```

2. 生成配置文件,跟着终端中的提示，按照自身需求一步步选择即可。

```bash
npm init @eslint/config
# or
yarn create @eslint/config
```

3. 配置 GIT 提交钩子检测

```json
"lint-staged": {
    "**/*": "prettier --write --ignore-unknown", //格式化
    "src/*": "eslint --ext .js,.ts,.tsx"  //进行eslint校验
  },
```

## 代码规范之 CSS 规范

1. 安装依赖

```bash
npm install --save-dev stylelint stylelint-config-standard
```

2. 在项目的根目录中创建一个配置文件`.stylelintrc.json`，内容如下：

```json
{
  "extends": "stylelint-config-standard"
}
```

3. 解决与`prettier`配置的冲突

```bash
npm install --save-dev stylelint-config-prettier
```

4. 将下面配置复制到`.stylelintrc.json`中：

```json
{
  "extends": ["stylelint-config-standard", "stylelint-config-prettier"]
}
```

5. 在 git commit 阶段进行检测：

```json
"lint-staged": {
    "**/*": "prettier --write --ignore-unknown", //格式化
    "src/**.{js,jsx,ts,tsx}": "eslint --ext .js,.jsx,.ts,.tsx", //对js文件检测
    "**/*.{less,css}": "stylelint --fix" //对css文件进行检测
}
```

## 代码规范之自定义其他规范

- 命名规范
  - 变量的命名中应尽量减少缩写的情况发生，做到见名知意。
  - 明确函数意图，对于返回 true or false 的函数，最好以 should/is/can/has 开头
- 写注释
- 变量兜底
- 辅助函数必须是纯函数
- 优先使用函数式编程
- 优先使用函数式组件
- 组件复杂度
- 用错误边界
- 避免嵌套三元运算符
- 将列表组件封装成独立组件
- 避免嵌套渲染函数
- 组件/函数导入导出
  - 在文件头部导入，顺序依次为: 第三方库 > 公共组件/方法 > 非公共部分组件/方法
  - 在底部导出
