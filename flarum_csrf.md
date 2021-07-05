# flarum csrf 验证

**Flarum** 默认是开启了 `csrf` 验证的，但是请求方法是 ```'GET', 'HEAD', 'OPTIONS'``` 这三种的时候是不验证的。

具体的 `CSRF` 验证文件在：```vendor/flarum/core/src/Http/Middleware/CheckCsrfToken.php``` 。



这里我们只说要验证的情况下，有时候我们需要取消 `csrf` 验证，比如说跟第三方外部接口对接的时候。

方法一：

> 请求时设置属性 `bypassCsrfToken` 为 `true` ，默认是 `false` 。
>
> 例如：`$request->withAttribute('bypassCsrfToken', true);`



方法二：

在 `extend.php` 文件中用 `Extend` 拓展，适合单个或者少量接口。

> ```php
> (new Flarum\Extend\Csrf())
> ->exemptRoute('your.api.name')
> ->exemptRoute('your.api.name2'),
> ```



方法三：

在 `extend.php` 文件中用 `Extend` 拓展，替换身份认证中间件让全部接口都不做 `csrf` 验证，可能会有安全风险的喔。

身份认证文件：

> vendor/flarum/core/src/Http/Middleware/AuthenticateWithHeader.php

在 `Extend` 拓展中替换这个中间件：

```php
//替换了这个身份认证中间件的话，那就要你自己写 `header` 的身份认证的喔！
//最朴实无华的方法是直接复制 `AuthenticateWithHeader.php` 来改一改。
(new Flarum\Extend\Middleware('api'))
        ->replace(Flarum\Http\Middleware\AuthenticateWithHeader::class,
            \Your\Middleware\NotCheckCsrfTokenMiddleware::class),
```

在自己定义的 `NotCheckCsrfTokenMiddleware`  这个中间件里面其实很简单；

按照中间件的写法设置一下 `bypassCsrfToken` 的属性即可，回到了**方法一**。

文件名 `NotCheckCsrfTokenMiddleware.php` ，代码如下：

```php
<?php

namespace Your\Middleware;

use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Server\RequestHandlerInterface;
use Psr\Http\Server\MiddlewareInterface;

class NotCheckCsrfTokenMiddleware implements MiddlewareInterface
{
    /**
     * @inheritDoc
     */
    public function process(ServerRequestInterface $request, RequestHandlerInterface $handler): ResponseInterface
    {
        // TODO: Implement process() method.
        /**
         * bypass CsrfToken
         */
        $request = $request->withAttribute('bypassCsrfToken', true);

        $response = $handler->handle($request);
        // Logic to run after the request is processed.
        return $response;
    }
}
```

