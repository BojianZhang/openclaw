# Component Mapping

把旧模板 section 映射成现代可复用组件：

## 常见映射
- old header/nav -> `SiteHeader`
- old hero/banner -> `HeroSection`
- services/features -> `FeatureGrid`
- portfolio/gallery -> `PortfolioGrid` / `GallerySection`
- testimonials -> `TestimonialSection`
- pricing -> `PricingSection`
- contact form -> `ContactSection`
- footer -> `SiteFooter`

## 输出方式
建议输出：
1. 页面骨架
2. 组件列表
3. 每个组件的职责
4. 哪些地方只继承结构，不继承代码

## 警告
- 不要直接把 legacy section 原样包装成“组件”就算完成
- 组件化不是 div 改名，而是职责明确、边界清楚、可替换
