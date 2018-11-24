# Server-Side Rendering

## Why SSR

1. SEO: Google 和 Bing 可以很好对同步 JavaScript 应用程序进行索引。在这里，同步是关键。如果你的应用程序初始展示 loading 菊花图，然后通过 Ajax 获取内容，抓取工具并不会等待异步完成后再行抓取页面内容。大多数搜索引擎包括百度都没有支持。
2. 加在速度： Faster Time-To-Content。