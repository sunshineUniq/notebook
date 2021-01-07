```json
{
    "editor.fontSize": 18,
    "editor.tabSize": 2,
    "editor.multiCursorModifier": "ctrlCmd",
    "editor.snippetSuggestions": "top",
    "editor.wordWrap": "on",
    "editor.formatOnSave": true,
    "workbench.iconTheme": "vscode-icons",
    "workbench.startupEditor": "newUntitledFile",
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true
        // "**/node_modules": true
    },
    "files.associations": {
        "*.wxml": "xml",
        "*.wxss": "css",
        "*.sass": "css",
        "*.wpy": "vue",
        "*.vue": "vue"
    },
    "emmet.includeLanguages": {
        "vue-html": "html",
        "javascript": "javascriptreact",
        "postcss": "css"
    },
    "emmet.triggerExpansionOnTab": true,
    "emmet.showSuggestionsAsSnippets": true,
    // 禁止 vetur 校验模版
    "vetur.validation.template": false,
    "vetur.format.defaultFormatterOptions": {
        "js-beautify-html": {
            "wrap_attributes": "force-expand-multiline"
        },
        "prettyhtml": {
            "printWidth": 100,
            "singleQuote": false,
            "wrapAttributes": false,
            "sortAttributes": false
        },
        "prettier": {
            "semi": false,
            "singleQuote": true
        }
    },
    "eslint.enable": true,
    "eslint.autoFixOnSave": true,
    "eslint.validate": [
        {
            "language": "html",
            "autoFix": true
        },
        {
            "language": "javascript",
            "autoFix": true
        },
        {
            "language": "javascriptreact",
            "autoFix": true
        },
        {
            "language": "vue",
            "autoFix": true
        }
        // "vue"
    ],
    // 配置以下两个，任意打开文件都可以使用ESLint来检查代码风格
    // 配置全局 eslint 包地址
    // "eslint.nodePath": "F:/devFiles/devToolsSettings/node_modules",
    // 配置全局 eslint 配置
    // "eslint.options": {
    //   "configFile": "F:\\devFiles\\devToolsSettings\\.eslintrc.js"
    // },
    "prettier.singleQuote": true,
    "prettier.semi": false,
    "prettier.disableLanguages": [
        "markdown"
    ],
    "extensions.autoUpdate": false,
    "vetur.format.defaultFormatter.html": "none",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\system32\\cmd.exe",
    "diffEditor.ignoreTrimWhitespace": true,
    // 配React的配置
    // emmet关于react的配置
    "emmet.syntaxProfiles": {
        "JavaScript React": "jsx"
    },
    "terminal.integrated.rendererType": "dom"
}
```