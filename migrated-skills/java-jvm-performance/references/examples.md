# Examples

## Example 1: Frequent Full GC

User asks:
- 线上服务 Full GC 很频繁，但没直接 OOM，这种一般怎么查？

Expected response shape:
1. Clarify symptom and required evidence.
2. Check old-gen pressure, allocation bursts, and retention pattern.
3. Explain why increasing heap is not automatically the first fix.
4. Give a stepwise diagnosis path.

## Example 2: High latency blamed on GC

User asks:
- 接口 RT 很高，是不是 JVM 参数要调一下？

Expected response shape:
1. Push back on premature tuning.
2. Separate GC, lock contention, downstream I/O, and CPU hotspots.
3. Ask for metrics, pauses, thread signals, and latency distribution.
4. Recommend evidence-first tuning.

## Example 3: OOM after traffic growth

User asks:
- 流量上来以后开始 OOM，怎么判断是泄漏还是容量不够？

Expected response shape:
1. Distinguish retention issue from expected working-set growth.
2. Ask for heap trend, dump, and retained object evidence.
3. Explain why heap expansion may only mask the issue.
4. Suggest the smallest useful next steps.
