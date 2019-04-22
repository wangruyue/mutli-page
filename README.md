# multi-page

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run all tests
npm test
```
# 搭建多页应用修改的地方 * 注意项目目录结构
# 版本号  vue 2.9.6 webpack 3.6.0 
# 1、修改unit文件
>  在unit 文件里添加获取公共文件路径的方法 getEntries
>   PS： 传hml 获取的html文件，传js 获取的js文件
# 2、修改 webpack.base 文件 即配置多页面入口
>   调用 getEntries（）方法 获取 入口文件 PS：传的是js文件目录 
>   utils.getEntries('./src/page/**/*.js')
# 3、修改webpack.dev.conf 文件 
>   调用 getEntries（）方法 获取渲染模板 PS：传的是html文件目录
>     utils.getEntries('./src/page/**/*.html')
   修改devserver属性
      这是单页面的配置，意思是所有访问路径都走index.html模板
        historyApiFallback: {
          rewrites: [
            { from: /.*/, to: path.posix.join(config.dev.assetsPublicPath, 'index.html') },
          ],
        },

      配置多页面需要改为，不同路径渲染不同的模板 即
        historyApiFallback: {
          rewrites: [
            PS: '/src/page/home/home' 是相对路径
            { from: /^\/page\/home/, to: '/src/page/home/home') }, 
            { from: /./, to: path.posix.join(config.dev.assetsPublicPath, 'index.html') },
          ],
        },

      配置 HtmlWebpackPlugin 渲染模板
        这里我保留里 根目录的 index 渲染模板
        调用方法pack（）循环添加 HtmlWebpackPlugin 
        pack（）里也有配置了  historyApiFallback.rewrites
        这样就不用手动添加了
      
 # 4、修改webpack.prod.conf 文件
 >     和dev文件类似，只是少了 devserver 的配置


    
