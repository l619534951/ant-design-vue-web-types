# （临时解决方案）生成ant-design-vue的web-types.json文件，用于代码提示，不让代码检查出现警告

## Project setup
```
1、npm install
2、npm update
3、npm run serve
4、打开浏览器，复制生成的json内容
5、在需要代码提示的项目的node_modules/ant-design-vue/dist目录下新建web-types.json
6、粘贴第4步的内容到web-types.json文件中
7、node_modules/ant-design-vue/package.json文件新增一项"web-types": "dist/web-types.json"
8、重新打开项目，有代码提示了
注意不要使用cnpm，会启动不起来
```

