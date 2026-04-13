# Examples

## Example 1: God service split

User asks:
- 这个 OrderService 已经 2000 行了，查询、校验、扣库存、发消息都写在一起，怎么拆？

Expected response shape:
1. Name the smell: god service and mixed responsibilities.
2. Separate concerns into orchestration, domain rule evaluation, persistence interaction, and event publishing.
3. Suggest the smallest safe refactor first:
   - extract validation logic
   - extract inventory policy
   - isolate message publishing boundary
4. Give a phased migration plan instead of a rewrite.

## Example 2: Pattern selection

User asks:
- 订单不同类型走不同定价逻辑，这里该不该上策略模式？

Expected response shape:
1. State when Strategy is justified.
2. Check whether the variation is stable and likely to grow.
3. Compare against a simpler conditional approach.
4. Recommend Strategy only if it reduces branching and future change cost.

## Example 3: Legacy refactor planning

User asks:
- 老项目想重构，但又怕影响线上行为，怎么推进？

Expected response shape:
1. Start with behavior-preserving goals.
2. Add characterization tests or capture representative cases.
3. Refactor by seam, not by whole-module rewrite.
4. Give stop conditions and rollback thinking.
