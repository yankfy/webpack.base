# 从Webpack3.0小白到大神
---
# 配置：入口和出口
```js
// 引入path
const path = require('path')

module.exports = {
    // 入口配置项
    entry:{
        // 名字随便写,多入口文件
        entry:"./src/entry.js",
        entry2:"./src/entry2.js"
    },
    // 出口配置项
    output:{
        path:path.resolve(__dirname,'dist'),
        // name表示名字与入口文件一样
        filename:"[name].js"
    },
    // 模块配置项
    module:{

    },
    // 插件功能项数组
    plugins:[

    ],
    // 开发服务
    devServer:{

    }
}
```
---
# 服务和热更新
```js
// 引入path
const path = require('path')

module.exports = {
    // 入口配置项
    entry:{
        entry:"./src/entry.js",
        entry2:"./src/entry2.js"
    },
    // 出口配置项
    output:{
        path:path.resolve(__dirname,'dist'),
        // name表示名字与入口文件一样
        filename:"[name].js"
    },
    // 模块配置项
    module:{

    },
    // 插件功能项数组
    plugins:[

    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer:{
        contentBase:path.resolve(__dirname,'dist'),
        host:'192.168.3.3', // 一般写ip地址,不写localhost
        compress:true,// 服务器压缩
        port:8888
    }
}

// 在package.json中写脚本语句
// "scripts": {
//     "server":"webpack-dev-server"
// }
```
---
# 打包CSS
```js
// 引入path
const path = require('path')

module.exports = {
    // 入口配置项
    entry: {
        // 名字随便写,多入口文件
        entry: "./src/entry.js",
        entry2: "./src/entry2.js"
    },
    // 出口配置项
    output: {
        path: path.resolve(__dirname, 'dist'),
        // name表示名字与入口文件一样
        filename: "[name].js"
    },
    // 模块配置项
    module: {
        rules: [
            // 打包CSS 需安装 style-loader处理样式 css-loader处理标签
            {
                test:/\.css$/,
                // 写法1
                // use:['style-loader','css-loader'],
                // 写法2
                // loader:['style-loader','css-loader'],
                // 写法3
                use:[
                    {
                        loader:"style-loader"
                        // module:true 配置项
                    },{
                        loader:"css-loader"
                    }
                ]
                // 可选配置项
                // include:
                // exclude:
                // query:
            }
        ]
    },
    // 插件功能项数组
    plugins: [

    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer: {
        contentBase: path.resolve(__dirname, 'dist'),
        host: '192.168.3.3', // 一般写ip地址,不写localhost
        compress: true, // 服务器压缩
        port: 8888
    }
}
```
---
# 压缩JS代码（生产环境）
```js
// 引入path
const path = require('path')
// 压缩JS
const uglify = require('uglifyjs-webpack-plugin')

module.exports = {
    // 入口配置项
    entry: {
        // 名字随便写,多入口文件
        entry: "./src/entry.js",
        entry2: "./src/entry2.js"
    },
    // 出口配置项
    output: {
        path: path.resolve(__dirname, 'dist'),
        // name表示名字与入口文件一样
        filename: "[name].js"
    },
    // 模块配置项
    module: {
        rules: [
            // 打包CSS 需安装 style-loader处理样式 css-loader处理标签
            {
                test:/\.css$/,
                // 写法1
                // use:['style-loader','css-loader'],
                // 写法2
                // loader:['style-loader','css-loader'],
                // 写法3
                use:[
                    {
                        loader:"style-loader"
                        // module:true
                    },{
                        loader:"css-loader"
                    }
                ]
                // 可选配置项
                // include:
                // exclude:
                // query:
            }
        ]
    },
    // 插件功能项数组
    plugins: [
        // min
        new uglify()
    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer: {
        contentBase: path.resolve(__dirname, 'dist'),
        host: '192.168.3.3', // 一般写ip地址,不写localhost
        compress: true, // 服务器压缩
        port: 8888
    }
}
```
--- 
# HTML打包
```js
// 引入path
const path = require('path')
const webpack = require('webpack')
// 压缩JS
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
// HTML打包
const htmlPlugin = require('html-webpack-plugin')

module.exports = {
    // 入口配置项
    entry: {
        // 名字随便写,多入口文件
        entry: "./src/entry.js",
        entry2: "./src/entry2.js"
    },
    // 出口配置项
    output: {
        path: path.resolve(__dirname, 'dist'),
        // name表示名字与入口文件一样
        filename: "[name].js"
    },
    // 模块配置项
    module: {
        rules: [
            // 打包CSS 需安装 style-loader处理样式 css-loader处理标签
            {
                test:/\.css$/,
                // 写法1
                // use:['style-loader','css-loader'],
                // 写法2
                // loader:['style-loader','css-loader'],
                // 写法3
                use:[
                    {
                        loader:"style-loader"
                        // module:true
                    },{
                        loader:"css-loader"
                    }
                ]
                // 可选配置项
                // include:
                // exclude:
                // query:
            }
        ]
    },
    // 插件功能项数组
    plugins: [
        // min
        new UglifyJsPlugin(),
        // html打包
        new htmlPlugin({
            // 去掉双引号
            minify:{
                removeAttributeQuotes:true
            },
            // js hash缓存
            hash:true,
            template:'./src/index.html'
        })
    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer: {
        contentBase: path.resolve(__dirname, 'dist'),
        host: '192.168.3.3', // 一般写ip地址,不写localhost
        compress: true, // 服务器压缩
        port: 8888
    }
}
```

# CSS 中添加图片【1】
```js
npm install --save-dev file-loader url-loader
```
```js
// 引入path
const path = require('path')
const webpack = require('webpack')
// 压缩JS
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
// HTML打包
const htmlPlugin = require('html-webpack-plugin')

module.exports = {
    // 入口配置项
    entry: {
        // 名字随便写,多入口文件
        entry: "./src/entry.js",
        entry2: "./src/entry2.js"
    },
    // 出口配置项
    output: {
        path: path.resolve(__dirname, 'dist'),
        // name表示名字与入口文件一样
        filename: "[name].js"
    },
    // 模块配置项
    module: {
        rules: [
            // 打包CSS 需安装 style-loader处理样式 css-loader处理标签
            {
                test:/\.css$/,
                // 写法1
                // use:['style-loader','css-loader'],
                // 写法2
                // loader:['style-loader','css-loader'],
                // 写法3
                use:[
                    {
                        loader:"style-loader"
                        // module:true
                    },{
                        loader:"css-loader"
                    }
                ]
                // 可选配置项
                // include:
                // exclude:
                // query:
            },{
                test:/\.(png|jpg|gif)/,
                use:[{
                    loader:"url-loader",
                    // 小于5000字节是js中的base64，否则是生成的图片路径
                    // url-loader中包含file-loader功能，filer-loader处理路径问题
                    options:{
                        limit:5000
                    }
                }]
            }
        ]
    },
    // 插件功能项数组
    plugins: [
        // min
        new UglifyJsPlugin(),
        // html打包
        new htmlPlugin({
            // 去掉双引号
            minify:{
                removeAttributeQuotes:true
            },
            // js hash缓存
            hash:true,
            template:'./src/index.html'
        })
    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer: {
        contentBase: path.resolve(__dirname, 'dist'),
        host: '192.168.3.3', // 一般写ip地址,不写localhost
        compress: true, // 服务器压缩
        port: 8888
    }
}
```
--- 
# CSS分离和publicPath【2】
```js
// 引入path
const path = require('path')
const webpack = require('webpack')
// 压缩JS
const UglifyJsPlugin = require('uglifyjs-webpack-plugin')
// HTML打包
const htmlPlugin = require('html-webpack-plugin')
// 分离CSS
const extractTextPlugin = require('extract-text-webpack-plugin')

var website = {
    publicPath:"http://192.168.3.3:8888/" // 最后的/不能省掉
}

module.exports = {
    // 入口配置项
    entry: {
        // 名字随便写,多入口文件
        entry: "./src/entry.js",
        entry2: "./src/entry2.js"
    },
    // 出口配置项
    output: {
        path: path.resolve(__dirname, 'dist'),
        // name表示名字与入口文件一样
        filename: "[name].js",
        // 公用路径 路径链接变成绝对链接
        publicPath:website.publicPath
    },
    // 模块配置项
    module: {
        rules: [
            // 打包CSS 需安装 style-loader处理样式 css-loader处理标签
            {
                test: /\.css$/,
                // 写法1
                // use:['style-loader','css-loader'],
                // 写法2
                // loader:['style-loader','css-loader'],
                // 写法3
                // use:[
                //     {
                //         loader:"style-loader"
                //         // module:true
                //     },{
                //         loader:"css-loader"
                //     }
                // ]
                // 分离CSS
                use: extractTextPlugin.extract({
                    fallback: "style-loader",
                    use: "css-loader"
                })
                // 可选配置项
                // include:
                // exclude:
                // query:
            }, {
                test: /\.(png|jpg|gif)/,
                use: [{
                    loader: "url-loader",
                    // 小于5000字节是js中的base64，否则是生成的图片路径
                    // url-loader中包含file-loader功能，filer-loader处理路径问题
                    options: {
                        limit: 5000
                    }
                }]
            }
        ]
    },
    // 插件功能项数组
    plugins: [
        // min
        new UglifyJsPlugin(),
        // html打包
        new htmlPlugin({
            // 去掉双引号
            minify: {
                removeAttributeQuotes: true
            },
            // js hash缓存
            hash: true,
            template: './src/index.html'
        }),
        // 分离CSS
        new extractTextPlugin("/css/index.css")
    ],
    // 开发服务和热更新
    // 启动要安装webpack-dev-server
    devServer: {
        contentBase: path.resolve(__dirname, 'dist'),
        host: '192.168.3.3', // 一般写ip地址,不写localhost
        compress: true, // 服务器压缩
        port: 8888
    }
}
```
