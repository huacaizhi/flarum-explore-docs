# flarum config

**Flarum** 安装成功之后，在项目的根目录下就会生成 `config.php` 文件。

`config.php` 文件内容：

```json
<?php return array (
  'debug' => true,
  'database' =>
  array (
    'driver' => 'mysql',
    'host' => '127.0.0.1',
    'port' => 3306,
    'database' => 'flarum',
    'username' => 'root',
    'password' => '123456',
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'strict' => false,
    'engine' => NULL,
    'prefix_indexes' => true,
  ),
  'url' => 'http://www.domain.com',
  'paths' =>
  array (
    'api' => 'api',
    'admin' => 'admin',
  ),
  'headers' =>
  array (
    'poweredByHeader' => true,
    'referrerPolicy' => 'same-origin',
  )
);

```

> 简要说明

1. `debug` : 是否开启调试模式，开发的时候一般设置为  `true` ，默认  `false`。
2. `database` : 数据库连接信息。
3. `url` : 主页 URL。
4. `paths` : 访问路径。
5. `headers` 头信息。



在某些情况下，你需要获取 `config.php` 里的某个数组或者某个值；

又或者你在这个文件里新增了其他的配置项，需要获取在其他地方使用；

怎么办呢？哈哈哈哈，办法肯定是有的：

```php
<?php
use Illuminate\Contracts\Container\Container;

class SomeClass
{
    /**
     * @var Container
     */
    protected $container;

    /**
     * @param Container $container
     */
    public function __construct(Container $container)
    {
        $this->container = $container;
    }
    
    /**
     * {@inheritdoc}
     */
    public function someFunction()
    {
        //获取 debug 的值
        $this->container->get('flarum.config')->offsetGet('debug');
        
        //获取 database 数组
        $this->container->get('flarum.config')->offsetGet('database');
        
        //获取 headers 数组
        $this->container->get('flarum.config')->offsetGet('headers');
        
        //获取 xxx 你定义的值或数组
        $this->container->get('flarum.config')->offsetGet('xxx');
        
        //获取 config.php 之后你的其他处理逻辑
    }
}
```

> 除了 `offsetGet()` 方法，还有一些其他方法可调用 。
>
> 详情请看  ```vendor\flarum\core\src\Foundation\Config.php ```  这个文件。

