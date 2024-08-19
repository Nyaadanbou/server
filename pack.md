# 资源包使用流程

以下的根无特殊说明都指插件根目录！

## 生成资源包

使用 `/wakame resourcepack generate` 命令，根据根目录下 `assets` 目录的配置生成资源包，生成的资源包将存放于 `generated/` 目录。

## 资源包配置规则

Wakame 的资源包配置规则类似 Minecraft 原版，但又有所不同。

### 基本结构

```
assets/
├─ models/
│ ├─ short_sword/ # 可自定义
│ │ ├─ demo.json
├─ textures/
│ ├─ short_sword/ # 可自定义
│ │ ├─ demo.png
```

### 特殊配置文件夹

1. `bbmodels`：根据 bbmodel 文件生成模型。
2. `textures`：存放贴图文件（png），类似于 Minecraft 资源包配置。
3. `models`：存放模型文件（json），类似于 Minecraft 资源包配置，但 `textures.layer0` 的路径可直接写相对于 `assets/textures` 的路径。在物品配置中通过 `path` 引用。

## 上传资源包

使用 `/wakame resourcepack upload` 命令，根据配置文件中 `Service` 设定的规则，将 `generated/` 目录下已生成的资源包上传。

## 基本概念

- **变体（variant）**：表示 `NekoStack` 的不同形态。当 `NekoStack` 使用默认材质时，其变体为 `0`。变体变化时，材质也随之改变。

## 添加物品材质

1. 在物品配置中添加 `assets` 配置：
   - 对于简单单贴图物品（如苹果、木棍），指定 `variant` 和单个 `path`，`path` 为贴图相对路径。
     ```yaml
     assets:
       - variant: 0
         path: "models/item/short_sword/demo.json"
       - variant: 1
         path: "models/item/short_sword/demo_1.json"
     ```
   - 对于多贴图物品（如弓、钓竿），根据多贴图规则提供一个 `variant` 和对应的 `path` 组（如弓需 4 个贴图）。
     ```yaml
     assets:
       - variant: 0
         path:
           - "models/item/bow/demo.json"
           - "models/item/bow/demo_pulling_0.json"
           - "models/item/bow/demo_pulling_1.json"
           - "models/item/bow/demo_pulling_2.json"
     ```
2. 使用 `/wakame reload config` 重载插件配置。
3. 根据以上操作生成资源包。
4. 根据需要上传资源包。
