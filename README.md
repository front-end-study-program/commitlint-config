# commitlint-config

练习 commitlint 相关的练习项目

## commit type

| 类型     | 功能 | 描述                               |
| -------- | ---- | ---------------------------------- |
| feat     | 功能 | 新增功能，迭代项目需求             |
| fix      | 修复 | 修复缺陷，修复上一版本存在问题     |
| docs     | 文档 | 更新文档，仅修改文档不修改代码     |
| style    | 样式 | 变动格式，不影响代码逻辑           |
| refactor | 重构 | 重构代码，非新增功能也非修复缺陷   |
| perf     | 性能 | 优化性能，提高代码执行性能         |
| test     | 测试 | 新增测试，追加测试用例验证代码     |
| build    | 构建 | 更新构建，改动构建工具或外部依赖   |
| ci       | 脚本 | 更新脚本，改动 CI 或执行脚本配置   |
| chore    | 事务 | 变动事务，改动其他不影响代码的事务 |
| revert   | 回滚 | 回滚版本，撤销某次代码提交         |
| merge    | 合并 | 合并分支，合并分支代码到其他分支   |
| sync     | 同步 | 同步分支，同步分支代码到其他分支   |
| impr     | 改进 | 改进功能，升级当前功能模块         |

## commitizen

1. install

	```shell
 	pnpm i -D commitizen cz-conventional-changelog
	```

2. settings

	```json
	{
		"script": {
			"commit": "git-cz"
		},
		"config": {
			"commitizen": {
				"path": "node_modules/cz-conventional-changelog"
			}
		}
	}
	```

3. used

	```shell
	npm run commit // 替代 git commit
	```

## commitlint (推荐)

### commit-msg 配置

1. install

	```shell
	pnpm i -D husky @commitlint/cli @commitlint/config-conventional
	```

2. settings

	2.1 在根目录下创建 commitlint.config.js 文件，配置如下：

	```js
	// commitlint.config.js
	module.exports = {
		extends: ["@commitlint/config-conventional"]
	}
	```

	2.2 在终端运行以下命令，生成 husky 的 commit-msg 钩子拦截，会在 git commit 的时候运行 commitlint 的命令进行 commit 提交信息验证

	``` shell
	npx husky add .husky/commit-msg "npx --no-install commitlint -e $HUSKY_GIT_PARAMS"
	```

### pre-commit 配置

1. install

	```shell
	pnpm i lint-staged husky -D
	```

2. settings
	2.1 在 package.json 文件中配置格式化的脚本命令以及配置需要检查的文件

	```json
	// package.json
	{
		"script": {
			"lint": "eslint --fix"
		},
		"lint-staged": {
			"**/*.{js,jsx,tsx,ts}": [
				"npm run lint"
			],
		}
	}
	```

	2.2 在终端运行以下命令，生成 husky 的 pre-commit 钩子拦截，会在 git commit 之前执行 npx --no -- lint-staged 命令来执行 npm run lint 进行代码检查。

	```shell
	npx husky add .husky/pre-commit "npx --no -- lint-staged"
	```
