# disqusjs-proxy-example

一个使用 [vercel](https://vercel.com/)*（前ZEIT Now）* 部署 Disqus API Proxy 的示例。

## 简介

Vercel 提供 Serverless 部署服务，支持包括静态网页、微服务、Lambda、持续集成等。在这里我们使用 Vercel 的微服务功能部署一个 Disqus API 的反代。

[DisqusJS](https://github.com/SukkaW/DisqusJS) 中提供的公共 Disqus API 反代就部署在 ZEIT Now 上。

## 使用教程

1. fork 这个 repo
2. 在 Vercel  上注册账号并绑定 GitHub 账号
3. 在 [GitHub APP](https://github.com/settings/installations) 中为 Now 设置你 fork 后的 repo 的访问权限
4. 在你 fork 后的 repo 中修改 `vercel.json` 的相关内容
  - 如果你想要绑定你自己的域名，请将 `vercel.json` 中 `duosuo.nobige.cn` 改成你的代理域名，或者你可以将整个 `alias` 字段删除
  - 如果不配置自己的域名，你也可以使用 vercel 提供的 `vercel.app` 子域名
  - 将 `cache-control` 的值为缓存时长（数字），单位是秒。默认为6个小时，可以按需要修改，如果你并不需要设置缓存 ，可以将其字段删除
  - `Access-Control-Allow-Origin`是设置跨域，值为你博客的域名，如博客域名为 `nobige.cn` 值则为 `https://nobige.cn` 或者是没有使用https的 `http://nobige.cn`
  - 如果你想要定制其它内容（如添加响应头），请参阅 [Vercel 的相关文档](https://vercel.com/docs/introduction)
5. 提交 commit
6. Vercel 会自动开始部署你的项目，当部署完成后，Vercel 的 Bot 会给你发送邮箱提示完成情况
7. 如果你绑定了你自己的域名，可以根据Vercel 的设置提示进行添加
8. 测试你的反代是否可以使用：访问你的反代域名，应该会跳转到 Disqus API 文档页面*（未使用魔法上网无法打开）*
  > 因为直接访问 https://disqus.com/api/ 便会跳转到 https://disqus.com/api/docs/ ；反代也会返回 3xx 状态码
9. 修改你的服务中 Disqus API Endpoint 的配置；如果你正在使用 [DisqusJS](https://github.com/SukkaW/DisqusJS)，这个配置是 DisqusJS 中的 `api` 字段。

## 注意事项

- Vercel 提供永久免费的 Plan，但是有 100GB 的流量限制
- Vercel 实例中的 `Vercel.app` 域名会使用 Cloudflare 的 Enterprise Plan；但是你绑定的自己的域名只能使用 Vercel 自有的基础设施，如有必要可以在实例之外套一层 CDN

