1. ```npm install xxx --save``` 和 ```--save-dev```

   > ```--save``` ：将模块安装到项目目录下，并在package文件的dependencies节点写入依赖
   >
   > ```--save-dev``` ：将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖



2. ```json
   // package.json
   "scripts": {
       "start": "node ./bin/www",
       "build":"webpack"
    }
   ```

   ```shell
   npm start
   npm run build
   # 为什么一个有run，一个没有run
   ```

   > `npm test`, `npm start`, `npm restart`, and `npm stop` are all aliases for `npm run ...`
   >
   > For all other `scripts` you define, you need to use the `npm run ...` syntax
   >
   > **test、start、restart、stop前面可以省略run，但是其他的都需要加上run**  [参考资料](<https://stackoverflow.com/questions/51358235/difference-between-npm-start-and-npm-run-start/51358329>)

