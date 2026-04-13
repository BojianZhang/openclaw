# Refactor Strategy

## Default Workflow

1. 先看模板类型
- 企业官网
- Agency
- 产品展示
- 作品集
- 摄影站
- 行业模板

2. 再看是否值得救
重点看：
- 信息架构是否清晰
- section 是否完整
- 页面是否有重复模式
- 是否只是视觉噪音堆砌

3. 拆结构
优先拆：
- header / nav
- hero
- features / services
- portfolio / gallery
- testimonials
- pricing
- contact / footer

4. 判断处理方式
- 保留结构：信息层级、版式节奏、栏目顺序
- 重写实现：HTML 结构、CSS、JS、响应式
- 直接丢弃：过时动画、Flash、旧插件、杂乱脚本

5. 输出现代化方案
- 页面骨架
- section 列表
- 可组件化部分
- 不建议继承的遗留部分
