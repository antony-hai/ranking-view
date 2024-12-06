### taro 开发小程序  H5

关于taro-cli脚手架模版拉下来的vite打包版本没有解决小程序UI库的打包问题，会导致编译出的代码在小程序平台上报错，这个版本换成webpack打包，解决vite打包的诸多问题。

启动流程
```javascrpt
  git clone https://github.com/antony-hai/taro-ranking.git
```
进入项目安装依赖，使用pnpm,确保nodejs版本在16以上
```javascrpt
  pnpm install
```

H5开发
```javascrpt
  npm run dev:h5
```

wx小程序开发
```javascrpt
  npm run dev:weapp
```
