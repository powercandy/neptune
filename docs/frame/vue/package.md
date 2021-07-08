
# vue仓库配置文件package.json


## package.json文件解析

```json
    {
        // 包名
        "name": "vue",
        // 版本
        "version": "2.6.9",
        // 描述
        "description": "Reactive, component-oriented view layer for modern web interfaces.",
        // CJS入口
        "main": "dist/vue.runtime.common.js",
        // ESM入口
        "module": "dist/vue.runtime.esm.js",
        // unpkg - CDN资源入口
        "unpkg": "dist/vue.js",
        // jsdelivr - CDN资源入口
        "jsdelivr": "dist/vue.js",
        // TS入口
        "typings": "types/index.d.ts",
        // 包含文件
        "files": [
            "src",
            "dist/*.js",
            "types/*.d.ts"
        ],
        // 是否包含副作用，优化tree-shaking
        "sideEffects": false,
        // 命令脚本
        "scripts": {
            "dev": "rollup -w -c scripts/config.js --environment TARGET:web-full-dev",
            "dev:cjs": "rollup -w -c scripts/config.js --environment TARGET:web-runtime-cjs-dev",
            "dev:esm": "rollup -w -c scripts/config.js --environment TARGET:web-runtime-esm",
            "dev:test": "karma start test/unit/karma.dev.config.js",
            "dev:ssr": "rollup -w -c scripts/config.js --environment TARGET:web-server-renderer",
            "dev:compiler": "rollup -w -c scripts/config.js --environment TARGET:web-compiler ",
            "dev:weex": "rollup -w -c scripts/config.js --environment TARGET:weex-framework",
            "dev:weex:factory": "rollup -w -c scripts/config.js --environment TARGET:weex-factory",
            "dev:weex:compiler": "rollup -w -c scripts/config.js --environment TARGET:weex-compiler ",
            "build": "node scripts/build.js",
            "build:ssr": "npm run build -- web-runtime-cjs,web-server-renderer",
            "build:weex": "npm run build -- weex",
            "test": "npm run lint && flow check && npm run test:types && npm run test:cover && npm run test:e2e -- --env phantomjs && npm run test:ssr && npm run test:weex",
            "test:unit": "karma start test/unit/karma.unit.config.js",
            "test:cover": "karma start test/unit/karma.cover.config.js",
            "test:e2e": "npm run build -- web-full-prod,web-server-basic-renderer && node test/e2e/runner.js",
            "test:weex": "npm run build:weex && jasmine JASMINE_CONFIG_PATH=test/weex/jasmine.js",
            "test:ssr": "npm run build:ssr && jasmine JASMINE_CONFIG_PATH=test/ssr/jasmine.js",
            "test:sauce": "npm run sauce -- 0 && npm run sauce -- 1 && npm run sauce -- 2",
            "test:types": "tsc -p ./types/test/tsconfig.json",
            "lint": "eslint src scripts test",
            "flow": "flow check",
            "sauce": "karma start test/unit/karma.sauce.config.js",
            "bench:ssr": "npm run build:ssr && node benchmarks/ssr/renderToString.js && node benchmarks/ssr/renderToStream.js",
            "release": "bash scripts/release.sh",
            "release:weex": "bash scripts/release-weex.sh",
            "release:note": "node scripts/gen-release-note.js",
            "commit": "git-cz"
        },
        // Git钩子
        "gitHooks": {
            // 对commit的内容进行校验
            "pre-commit": "lint-staged",
            // 对commit信息进行校验
            "commit-msg": "node scripts/verify-commit-msg.js"
        },
        // commit前内容进行eslint校验和修复并将提交的内容提交至Git暂存区
        "lint-staged": {
            "*.js": [
            "eslint --fix",
            "git add"
            ]
        },
        // 仓库信息
        "repository": {
            // 仓库类型
            "type": "git",
            // 仓库地址
            "url": "git+https://github.com/vuejs/vue.git"
        },
        // 该Npm包的关键字
        "keywords": [
            "vue"
        ],
        // 作者
        "author": "Evan You",
        // 证书
        "license": "MIT",
        // Bugs信息
        "bugs": {
            // 提交Bug地址
            "url": "https://github.com/vuejs/vue/issues"
        },
        // 主页地址
        "homepage": "https://github.com/vuejs/vue#readme",
        // 开发依赖
        "devDependencies": {
            "@babel/core": "^7.0.0",
            "@babel/plugin-proposal-class-properties": "^7.1.0",
            "@babel/plugin-syntax-dynamic-import": "^7.0.0",
            "@babel/plugin-syntax-jsx": "^7.0.0",
            "@babel/plugin-transform-flow-strip-types": "^7.0.0",
            "@babel/preset-env": "^7.0.0",
            "@babel/register": "^7.0.0",
            "@types/node": "^10.12.18",
            "@types/webpack": "^4.4.22",
            "acorn": "^5.2.1",
            "babel-eslint": "^10.0.1",
            "babel-helper-vue-jsx-merge-props": "^2.0.3",
            "babel-loader": "^8.0.4",
            "babel-plugin-istanbul": "^5.1.0",
            "babel-plugin-transform-vue-jsx": "^4.0.1",
            "babel-preset-flow-vue": "^1.0.0",
            "buble": "^0.19.3",
            "chalk": "^2.3.0",
            "chromedriver": "^2.45.0",
            "codecov": "^3.0.0",
            "commitizen": "^2.9.6",
            "conventional-changelog": "^1.1.3",
            "cross-spawn": "^6.0.5",
            "cz-conventional-changelog": "^2.0.0",
            "de-indent": "^1.0.2",
            "es6-promise": "^4.1.0",
            "escodegen": "^1.8.1",
            "eslint": "^5.7.0",
            "eslint-plugin-flowtype": "^2.34.0",
            "eslint-plugin-jasmine": "^2.8.4",
            "file-loader": "^3.0.1",
            "flow-bin": "^0.61.0",
            "hash-sum": "^1.0.2",
            "he": "^1.1.1",
            "http-server": "^0.11.1",
            "jasmine": "^2.99.0",
            "jasmine-core": "^2.99.0",
            "karma": "^3.1.1",
            "karma-chrome-launcher": "^2.1.1",
            "karma-coverage": "^1.1.1",
            "karma-firefox-launcher": "^1.0.1",
            "karma-jasmine": "^1.1.0",
            "karma-mocha-reporter": "^2.2.3",
            "karma-phantomjs-launcher": "^1.0.4",
            "karma-safari-launcher": "^1.0.0",
            "karma-sauce-launcher": "^2.0.2",
            "karma-sourcemap-loader": "^0.3.7",
            "karma-webpack": "^4.0.0-rc.2",
            "lint-staged": "^8.0.0",
            "lodash": "^4.17.4",
            "lodash.template": "^4.4.0",
            "lodash.uniq": "^4.5.0",
            "lru-cache": "^5.1.1",
            "nightwatch": "^0.9.16",
            "nightwatch-helpers": "^1.2.0",
            "phantomjs-prebuilt": "^2.1.14",
            "puppeteer": "^1.11.0",
            "resolve": "^1.3.3",
            "rollup": "^1.0.0",
            "rollup-plugin-alias": "^1.3.1",
            "rollup-plugin-buble": "^0.19.6",
            "rollup-plugin-commonjs": "^9.2.0",
            "rollup-plugin-flow-no-whitespace": "^1.0.0",
            "rollup-plugin-node-resolve": "^4.0.0",
            "rollup-plugin-replace": "^2.0.0",
            "selenium-server": "^2.53.1",
            "serialize-javascript": "^1.3.0",
            "shelljs": "^0.8.1",
            "terser": "^3.10.2",
            "typescript": "^3.1.3",
            "webpack": "~4.28.4",
            "weex-js-runtime": "^0.23.6",
            "weex-styler": "^0.3.0",
            "yorkie": "^2.0.0"
        },
        // 该包脚本命令使用的参数配置
        "config": {
            "commitizen": {
            "path": "./node_modules/cz-conventional-changelog"
            }
        }
    }
```
