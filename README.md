# flarum-explore-docs

机缘巧合之下，接触到基于 `flarum` 论坛程序并进行二次开发，整理了一些开发资料，不是最佳实践哈。

Some documents for redevelopment using flarum, It's not a best practice.

  

##### 文档适用的 `flarum` 版本

**Flarum 0.1.0-beta.16**

> 通过在项目根目录下执行 `php flarum --version` 查看 `flarum` 版本
>
> 按理说应该跟 `Flarum 1.0.0` 版本差不多，当时刚安装上 `beta.16` 然后没过几天就发布了 `Flarum 1.0.0`

  

##### `Flarum` 安装

安装在 flarum 目录：```composer create-project flarum/flarum flarum```

安装在当前所在目录：```composer create-project flarum/flarum .```

更多详细请参考：https://docs.flarum.org/install.html

  

##### 文档目录

1. 核心目录 [flarum_core](./flarum_core.md)
2. 认证 [authentication](./flarum_authentication.md)
3. 配置文件 [config](./flarum_config.md)
4. Csrf 验证 [Csrf 验证](./flarum_csrf.md)

  

##### 参考资料（包括不限于）

> 官网：https://flarum.org/
>
> 官网文档（英文）：https://docs.flarum.org/
>
> 中文文档（未完全翻译）：https://flarum.org.cn/
>
> flarum 代码仓库：https://github.com/flarum/core
>
> flarum 代码仓库文档（很重要）：https://github.com/flarum/docs

> Flarum 文档1：https://www.bookstack.cn/read/flarum-doc/README.md
>
> Flarum 文档2：http://php.szlt.net/flarum/index.html