<h1 align="center">commitlint-config-cmyr </h1>
<p>
  <a href="https://www.npmjs.com/package/commitlint-config-cmyr" target="_blank">
    <img alt="Version" src="https://img.shields.io/npm/v/commitlint-config-cmyr.svg">
  </a>
  <a href="https://github.com/CaoMeiYouRen/commitlint-config-cmyr/actions?query=workflow%3ARelease" target="_blank">
    <img alt="GitHub Workflow Status" src="https://img.shields.io/github/actions/workflow/status/CaoMeiYouRen/commitlint-config-cmyr/release.yml?branch=master">
  </a>
  <img src="https://img.shields.io/badge/node-%3E%3D18-blue.svg" />
  <a href="https://github.com/CaoMeiYouRen/commitlint-config-cmyr#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/CaoMeiYouRen/commitlint-config-cmyr/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
  <a href="https://github.com/CaoMeiYouRen/commitlint-config-cmyr/blob/master/LICENSE" target="_blank">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
  </a>
</p>

> 草梅友仁自定义的 commitlint 配置 - 一个更符合中文环境使用习惯的提交信息规范

## 🚀 特性

-   🌏 **中文友好**: 完整的中文提示和描述
-   🎨 **表情符号**: 为每种提交类型配置了对应的 emoji
-   🔧 **合理默认**: 基于 Conventional Commits 规范，但更加宽松
-   ⚡ **开箱即用**: 简单配置即可使用
-   📝 **交互式提交**: 支持 commitizen 交互式提交

## 🎯 支持的提交类型

| 类型       | 描述         | Emoji |
| ---------- | ------------ | ----- |
| `feat`     | 新功能       | ✨    |
| `fix`      | 错误修复     | 🐛    |
| `docs`     | 文档更改     | 📚    |
| `style`    | 代码样式更改 | 💎    |
| `refactor` | 代码重构     | 📦    |
| `perf`     | 性能优化     | 🚀    |
| `test`     | 测试相关     | 🚨    |
| `build`    | 构建相关     | 🛠     |
| `ci`       | CI/CD 相关   | ⚙️    |
| `chore`    | 其他杂项     | ♻️    |
| `revert`   | 回退提交     | 🗑     |

## 📋 依赖要求

-   Node.js >=18

## 📦 安装

### npm

```bash
npm install --save-dev commitlint-config-cmyr
```

### yarn

```bash
yarn add --dev commitlint-config-cmyr
```

### pnpm

```bash
pnpm add --save-dev commitlint-config-cmyr
```

## ⚙️ 配置使用

### 1. 安装 commitlint CLI

```bash
npm install --save-dev @commitlint/cli
```

### 2. 创建配置文件

在项目根目录下创建 `commitlint.config.js` 或 `commitlint.config.ts` 文件：

#### JavaScript 配置

```javascript
// commitlint.config.js
export default {
    extends: ["cmyr"],
};
```

#### TypeScript 配置

```typescript
// commitlint.config.ts
const Configuration: UserConfig = {
    extends: ["cmyr"],
};

export default Configuration;
```

### 3. 添加 Git Hooks（可选但推荐）

#### 使用 husky

安装 husky：

```bash
npm install --save-dev husky
npx husky install
```

添加 commit-msg hook：

```bash
npx husky add .husky/commit-msg 'npx commitlint --edit $1'
```

### 4. 配置交互式提交（可选）

如果想要使用交互式提交，需要安装 commitizen：

```bash
npm install --save-dev commitizen cz-conventional-changelog-cmyr
```

在 `package.json` 中添加：

```json
{
    "config": {
        "commitizen": {
            "path": "cz-conventional-changelog-cmyr"
        }
    },
    "scripts": {
        "commit": "cz"
    }
}
```

然后使用以下命令进行交互式提交：

```bash
npm run commit
```

## 📝 使用示例

### 有效的提交信息示例

```
feat: 添加用户登录功能

fix(auth): 修复登录验证失败的问题

docs: 更新API文档

style: 修复代码格式问题

refactor: 重构用户管理模块

perf: 优化数据库查询性能

test: 添加单元测试

build: 升级webpack配置

ci: 更新GitHub Actions工作流

chore: 更新依赖包版本

revert: 回退"添加用户登录功能"
```

## 🔧 自定义配置

如果需要自定义规则，可以在配置文件中覆盖默认规则：

```typescript
// commitlint.config.ts
import type { UserConfig } from "@commitlint/types";

const Configuration: UserConfig = {
    extends: ["commitlint-config-cmyr"],
    rules: {
        // 自定义提交类型
        "type-enum": [
            2,
            "always",
            [
                "feat",
                "fix",
                "docs",
                "style",
                "refactor",
                "perf",
                "test",
                "build",
                "ci",
                "chore",
                "revert",
                "custom", // 添加自定义类型
            ],
        ],
        // 自定义标题最大长度
        "header-max-length": [2, "always", 100],
        // 强制要求作用域
        "scope-empty": [2, "never"],
    },
};

export default Configuration;
```

## 📋 默认规则

此配置包含以下默认规则：

| 规则                     | 级别     | 配置   | 说明                        |
| ------------------------ | -------- | ------ | --------------------------- |
| `type-enum`              | error    | always | 限制提交类型在预定义列表中  |
| `subject-full-stop`      | disabled | never  | 不强制要求主题以句号结尾    |
| `subject-case`           | disabled | never  | 不限制主题大小写            |
| `body-max-line-length`   | disabled | never  | 不限制正文行长度            |
| `footer-max-line-length` | disabled | never  | 不限制页脚行长度            |
| `header-max-length`      | error    | 140    | 限制标题最大长度为 140 字符 |

## 🛠️ 开发相关

### 开发模式

```bash
npm run dev
```

### 构建项目

```bash
npm run build
```

### 代码检查

```bash
npm run lint
```

### 交互式提交

```bash
npm run commit
```

## 🤝 相关项目

-   [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) - 本配置基于此扩展
-   [cz-conventional-changelog-cmyr](https://github.com/CaoMeiYouRen/cz-conventional-changelog-cmyr) - 配套的 commitizen 适配器
-   [conventional-changelog-cmyr-config](https://github.com/CaoMeiYouRen/conventional-changelog-cmyr-config) - 配套的 changelog 配置

## 💡 为什么选择这个配置？

-   **中文环境友好**: 所有提示信息都是中文，便于团队使用
-   **合理的默认值**: 基于实际项目经验优化的规则配置
-   **灵活性**: 可以根据项目需要轻松自定义规则
-   **完整的工具链**: 配合其他工具形成完整的提交规范解决方案

## 📚 相关资源

-   [Conventional Commits 规范](https://www.conventionalcommits.org/zh-hans/)
-   [commitlint 官方文档](https://commitlint.js.org/)
-   [commitizen 使用指南](https://github.com/commitizen/cz-cli)

## 🔍 常见问题

### Q: 如何在现有项目中集成？

A: 按照上述配置步骤操作，如果项目已有 commitlint 配置，只需要将 extends 改为 `['commitlint-config-cmyr']` 即可。

### Q: 可以和其他 commitlint 配置同时使用吗？

A: 可以，配置会按照 extends 数组的顺序进行合并，后面的配置会覆盖前面的配置。

### Q: 如何禁用某些规则？

A: 在配置文件的 rules 中设置对应规则的级别为 0（禁用）即可。

## 👥 作者

👤 **CaoMeiYouRen**

-   Website: [https://blog.cmyr.ltd/](https://blog.cmyr.ltd/)
-   GitHub: [@CaoMeiYouRen](https://github.com/CaoMeiYouRen)

## 🤝 贡献

欢迎 贡献、提问或提出新功能！<br />如有问题请查看 [issues page](https://github.com/CaoMeiYouRen/commitlint-config-cmyr/issues). <br/>贡献或提出新功能可以查看[contributing guide](https://github.com/CaoMeiYouRen/commitlint-config-cmyr/blob/master/CONTRIBUTING.md).

## 💰 支持

如果觉得这个项目有用的话请给一颗 ⭐️，非常感谢

## 📝 License

Copyright © 2021 [CaoMeiYouRen](https://github.com/CaoMeiYouRen).<br />
This project is [MIT](https://github.com/CaoMeiYouRen/commitlint-config-cmyr/blob/master/LICENSE) licensed.

---

_This README was generated with ❤️ by [cmyr-template-cli](https://github.com/CaoMeiYouRen/cmyr-template-cli)_
