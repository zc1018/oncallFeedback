---
name: oncall-feedback-router
description: "Route XDF/OPE production-duty feedback. Use when the user provides a feedback/problem message plus a DingTalk/WeCom group, asks 值班反馈怎么处理, 是否需要建 TAPD, 该怎么回复, 是否升级, 找谁跟进, 如何闭环, or how to record/update 值班日技术工单list."
---

# Oncall Feedback Router

## Overview

Use this skill to turn "feedback content + source group" into a duty-handler action plan for XDF/OPE product R&D support. Answer in Chinese by default and focus on what the duty person should do now, what to record, and what to say back.

Source baseline: the DingTalk document `产研值班机制` as checked on 2026-06-17. If the user asks for the latest policy, exact current duty-table data, or a policy-sensitive case, refresh the source with `dws` before making a final call.

## Input Handling

Expect the user to provide:

- `反馈内容`: the message, screenshot text, symptom, or complaint.
- `所在群`: the DingTalk or WeCom group where it appeared.

If one is missing, still give a best-effort recommendation and list the missing information that would change the decision. Do not block on clarification unless the next action could create the wrong ticket, contact the wrong team, or expose sensitive information.

Do not reproduce passwords or private credentials from source documents. Refer to them as "文档指定的公共企微账号" or "找对应负责人获取".

## Decision Workflow

1. Identify the business line and channel from the group name.
2. Classify the issue: online system, offline system, cloud classroom/live replay, app feedback, permission/whitelist, student contact, common FAQ, or unknown.
3. Decide severity:
   - Important activity support: respond within 5 minutes.
   - Weekend/holiday duty issue: respond within 30 minutes.
   - Emergency candidate: core flows such as live/recorded class, ordering/payment, class start, registration/login fail, especially when the same issue has 3 reports within 2 hours.
4. Choose the handling path:
   - Use the work-order assistant robot for online business groups that have it.
   - Manually create a TAPD technical ticket for offline business or groups without a robot.
   - Route cloud classroom live/replay issues to Cloud Classroom 400 support.
   - For app feedback that requires manual TAPD entry, add the required `APP反馈` keyword when applicable.
   - For whitelist issues in groups where business teachers handle permissions, do not take over; acknowledge and point to the business-side owner.
5. Close the loop:
   - If solved today, sync the result to the reporter.
   - If not solved today, write current status and next owner in TAPD, transfer per the production issue process, and tell the reporter the follow-up path.
   - At end of duty, update the holiday duty table field `值班日技术工单list` and sync the duty group/stability owner.

For detailed routing rules and output examples, read `references/oncall-rules.md`.

## Output Format

Use this structure unless the user asks for a shorter answer:

```
处理结论：
- [一句话说明该不该由值班人处理、是否建单、是否升级]

马上做：
1. [第一步]
2. [第二步]
3. [第三步]

回复话术：
> [可直接发到群里的短回复]

工单/记录要点：
- 来源群：
- 问题现象：
- 影响范围：
- 处理动作：
- owner / 下一步：
- 是否已同步反馈人：

需要补充的信息：
- [只列会影响判断的信息；没有就写“无”]
```

Keep recommendations operational. Avoid long policy summaries unless the user asks why.
