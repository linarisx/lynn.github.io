## 工程路径
实际上就是Assets文件夹
**`Application.dataPath`**
只会在编辑时使用
游戏打包，该路径不存在

## Resources资源文件夹
**`Application.dataPath + "/Resources"`**
一般用API加载
动态加载资源放在里面
打包时文件夹内容会都打包出去，unity自动加密
打包后只能读

## streamingAssetsPath
不同平台得到的路径都是不一样的，所以不要拼接写
**`Application.streamingAssetsPath`**
移动平台只读，PC可读可写
打包出去不会被加密
可以放入自定义动态加载的初始资源（热更新，配置文件等）

## persistentDataPath
**`print(Application.persistentDataPath);`**
所有平台可读可写
固定数据文件夹
保存玩家数据，热更新下载资源，代码
放动态下载 / 创建的文件，游戏中创建 / 获取的文件

## Plugins文件夹
放插件

## Editor
放编辑器相关(一般不获取，可通过路径) 内容不会被打包出去

## Standard Assets
下载unity自带资源会自动创建，自己创建