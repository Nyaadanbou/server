# 资源包的使用流程

下面是关于资源包如何使用的具体逻辑.

## 资源包的生成

使用 `/wakame resourcepack generate` 将会根据插件根目录下的 `assets` 内的配置与物品配置, 在插件根目录下的 `generated/` 生成资源包.

## 资源包配置规则

Wakame 的资源包有着类似 Minecraft 原版但又独特的配置规则.

将会进行特定处理的配置文件夹:
  1. `bbmodels`: 将会根据 bbmodel 生成模型.
  2. `models`: 与 Minecraft 资源包配置类似, 但是 `textures` 内的路径可直接写贴图图片与 `assets` 的相对路径, 需在物品内通过 `path` 进行引用.
  3. `textures`: 与 Minecraft 资源包配置类似,

## 资源包的上传

使用 `/wakame resourcepack upload` 会根据具体配置文件内设置的 `Service` 将 `generated/` 下**已生成**的资源包根据特定规则上传.

## 一些基本概念

变体 \(varaint\): 表示一个 `NekoStack` 的多种不同形态, 当一个 `NekoStack` 是默认材质时, 他的变体永远是 `0`. 当 `NekoStack` 的变体发生变化时, 他的材质也会发生变化. 一个 `NekoStack` 与一个变体永远只会指向一个材质\(组\)

## 如何添加物品材质？

1. 在特定物品配置内添加 `assets` 配置, 配置规则如下:
    - 如物品为简单的单贴图物品\(如苹果, 木棍\), 则直接指定 `varaint` 与单个 `path`. `path` 则是贴图模型相对于插件根目录的 `assets` 路径.
        ```yaml
        assets:
          - variant: 0
            path: "models/item/short_sword/demo.json"
          - variant: 1
            path: "models/item/short_sword/demo_1.json"
          ...
        ```
   - 如物品为多贴图物品\(如弓, 钓竿\), 则需按此多贴图物品的模型规则来提供一个 `varaint` 一个特定数量 `path` 组\(如弓需要 `4` 个贴图\). `path` 则是贴图模型相对于插件根目录的 `assets` 路径.
       ```yaml
       assets:
         - variant: 0
           path:
             - "models/item/bow/demo.json"
             - "models/item/bow/demo_pulling_0.json"
             - "models/item/bow/demo_pulling_1.json"
             - "models/item/bow/demo_pulling_2.json"
         ...
       ```
2. 使用 `/wakame reload config` 来重载插件.
3. 根据上面的操作来生成资源包.
4. 到这里资源包已制作完毕, 可按需根据上面的操作来上传资源包.
