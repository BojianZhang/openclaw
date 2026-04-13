---
name: proxy-automation-stabilizer
description: Use when building, debugging, stabilizing, or speeding up proxy-driven browser automation projects such as Playwright/Puppeteer registration/login flows with homepage readiness issues, verification-code handling, session persistence, bad-proxy churn, or stage-level performance diagnosis. Triggers on requests to stabilize automation, reduce retries, improve proxy precheck quality, harden verification input, split run/test behavior, or turn project learnings into repeatable workflow.
---

# proxy-automation-stabilizer

适用于：
- 代理驱动的网站自动化
- 批量注册 / 登录 / 首屏进入类流程
- 使用 Playwright（或类似浏览器自动化）+ 代理 + 邮件验证码 / 会话持久化 的项目
- 当前问题重点是“流程能跑但不稳 / 代理浪费 / 页面慢 / 验证码输入不稳 / 失败分类混乱”时

## 核心原则

### 1. 先打通主链，再回补安全，再做提速
不要一开始就堆满失败检查、兜底逻辑、通用 fallback。正确顺序是：
1. 打通最短成功路径
2. 清掉会阻塞主流程的重检查
3. 统一关键阶段等待
4. 回补必要的安全检查（单次、轻量、非阻塞）
5. 最后做性能精修与代理治理

### 2. 预检通过 ≠ 业务可用
代理能通过 GET / CONNECT 预检，只代表网络可连，不代表业务页面真的能跑起来。
必须区分：
- 连通性预检：能否连上目标站点
- 业务健康预检：目标首页是否进入“可操作状态”

### 3. 失败分类不要阻塞主链
失败检查应该：
- 分阶段回补
- 尽量单次快查
- 尽量放在动作后补查，而不是动作前把主链堵死

### 4. run/test 必须分离
默认策略：
- run：更激进、更快、少截图、少等待、轻资源
- test：更保守、更可视、更多截图、更多观察时间

## 推荐工作流

## 阶段 A：打通最短成功路径
目标：先拿到一次稳定成功，不要先追求全面兜底。

检查顺序：
1. 首页能打开
2. 能进入核心表单 / 登录入口
3. 能提交关键表单
4. 能进入验证码阶段
5. 能输入验证码
6. 能进入后续页 / 拿到 cookie / session

此阶段要求：
- 避免复杂失败扫描
- 避免通用型宽泛 selector 池
- 先以最窄、最站点专用的路径跑通

## 阶段 B：清掉阻塞式检查
识别并移除：
- Continue 后的重型结果判定窗口
- 在 while 循环里反复跑的失败扫描
- 在验证码确认函数里混入的复杂失败检测
- 任何“为了保险”但会让主流程卡住的检查

规则：
- 等待函数只负责等待自己的目标状态
- 失败判断优先放到动作后单次补查

## 阶段 C：回补安全检查（单次、轻量、非阻塞）
推荐回补顺序：
1. Continue 后单次快查：
   - 已存在账号
   - 注册拒绝 / Try again later
2. 验证码提交后补查：
   - Wrong verification code
   - Verification code rate limited
   - 已存在账号
   - 注册拒绝 / IP 黑
3. 失败后重分类：
   - 不要只保留粗粒度“阶段失败”错误
   - 尽量重归类成真实业务原因

## 阶段 D：性能定位
性能问题必须拆阶段，不靠猜。

推荐拆分：
- 首页阶段
  - navDone
  - deadPageCheckDone
  - overlayDone
  - loginSignalDone
- 表单阶段
  - submitSignup.*
- 验证码 / 生日阶段
  - enterVerificationDone
  - waitBirthdayReadyDone
  - fillBirthdayDone
  - clickBirthdayNextDone
- 后置阶段
  - waitPostRegisterReadyDone
  - waitSessionCookieDone

#### 阶段化测速模板（可直接照搬）
- 首页：`openDreamina.navDone / deadPageCheckDone / overlayDone / loginSignalDone / attemptReady`
- 表单：`submitSignup.overlayPrepassDone / clickLoginEntryDone / postSignEntryWaitDone / clickContinueWithEmailDone / clickSignUpDone / fillEmailDone / fillPasswordDone / clickContinueDone`
- 验证码：`fetchVerificationCode` + `enterVerificationCode.*`
- 生日：`waitBirthdayReadyDone / fillBirthdayDone / clickBirthdayNextDone`
- 后置：`postBirthdayNext.waitPostRegisterReadyDone / postBirthdayNext.waitSessionCookieDone`

原则：
- 每次只拆当前最大黑盒
- 看日志后再决定下一刀，不要预先到处埋点
- 一旦某段已证明确实不慢，就停止继续细拆，转去下一段最大黑盒

## 阶段 E：代理治理

### 1. 两层预检
第一层：连通性预检
- GET 目标首页
- CONNECT / 状态码 / 出口 IP / 速度分层

第二层：轻量首页健康预检
- 打开首页
- 只判断是否进入可操作状态
- 不正式注册
- 不填账号
- 不走验证码

#### 轻量首页健康预检步骤（推荐最小实现）
1. 仅对“连通性预检通过”的代理继续执行
2. 用 Playwright / Puppeteer 启动最轻量浏览器上下文
3. 套用 run 模式轻量策略：
   - 默认拦截 `image / media / font`
   - 使用 run 级首页 dead-page grace wait
   - 使用 run 级登录信号等待节奏
4. 打开目标首页，仅检查是否进入“可操作状态”
5. 命中以下任一信号则判定为 homepage-health PASS：
   - `Sign in / Log in / Sign up`
   - `Continue with email`
   - `Enter email`
   - 站点特定登录/注册壳节点
6. 命中以下任一信号则判定为 homepage-health FAIL：
   - `DREAMINA_FIRST_LOAD_DEAD_PAGE`
   - `DREAMINA_WHITE_SCREEN`
   - shell 回来但伴随明显资源 / 脚本失败且首页不可操作
7. PASS 才允许进入正式注册池；FAIL 直接写 bad，不要混入正式账号任务

### 2. 运行期快速淘汰
以下信号默认视为“业务不可用代理”：
- DREAMINA_FIRST_LOAD_DEAD_PAGE
- DREAMINA_WHITE_SCREEN
- 明确 IP 黑 / signup rejected by proxy

动作：
- 立即从健康池移出
- 写入 bad
- 不要继续让当前账号反复吃同类坏代理

#### 快速淘汰规则（建议直接固化到 runner）
- 运行期一旦命中 `DREAMINA_FIRST_LOAD_DEAD_PAGE` / `DREAMINA_WHITE_SCREEN`，不要只记失败次数；优先直接按 hard proxy failure 处理
- 如果项目里存在“重试 3 次后抛统一错误”的逻辑，必须保留底层真实失败原因，避免 runner 因原因被吃掉而无法正确剔除坏代理
- 同一 host / 同一类代理若连续出现首页死页，可进一步做 host 级临时降权或整批暂停

### 3. 关键认知
- 预检通过 ≠ 可注册
- HTML 回来 ≠ 首屏可用
- 站点 shell 加载成功 ≠ JS/CSS/chunk 正常

## 验证码输入专项规则

### 1. 候选池必须白名单化
不要使用：
- 通用 textbox first()
- 宽泛 input 池
- 任意可见 div

优先使用：
1. 站点真实验证码 input
2. 专用 wrapper / focus 节点
3. 最后才是 fallback keyboard

### 2. 经验结论
候选池过宽会误命中非验证码 DOM，导致：
- fill/type/注入全部打空
- 表面像“拿到码但不填写”

## run/test 分离建议

### run
- 拦截 image / media / font
- 更短的 dead page grace wait
- 更激进的 login signal 轮询
- 截图默认关闭
- human pause 最小化

### test
- 保留更多观察时间
- 截图默认开启
- 页面尽量完整可视
- 轮询更保守

## 什么时候该停
当你已经满足：
- 主链稳定成功
- 主要失败原因可分类
- 阶段耗时已经能定位
- 继续优化只是在抠小量级波动

这时应优先：
- 提交当前成果
- 固化经验到文档 / skill / 注释
而不是继续无限堆 patch。

## 快速检查清单
- [ ] 主链是否已跑通一次真实成功
- [ ] Continue 后是否还有阻塞式失败检查
- [ ] 验证码候选池是否仍过宽
- [ ] 失败是否能重分类成真实业务原因
- [ ] 首页是否拆成 nav / deadPage / overlay / loginSignal
- [ ] 后半段是否拆到 cookie / ready 层级
- [ ] 代理是否区分“网络可连”和“业务可用”
- [ ] 业务不可用代理是否会被快速淘汰
- [ ] run/test 是否已分离
- [ ] 当前阶段是否应该收口提交
