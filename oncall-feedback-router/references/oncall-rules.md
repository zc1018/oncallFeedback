# Oncall Feedback Routing Rules

Use these rules after reading the user's feedback content and source group.

## Core SLA

- Important activity support: respond within 5 minutes.
- Weekend or holiday duty: respond within 30 minutes.
- Duty time baseline: 10:00-19:00.
- Every accepted issue must be closed-loop: solve, hand off, or record the next owner and current status.

## Channel Routing

| Signal | Handling |
|---|---|
| Online university business system, group has work-order assistant | Use the assistant robot to create or guide the work order. |
| Offline business line, 线下需求沟通问题处理群, or group without assistant robot | Manually create a TAPD technical ticket using the required template. |
| App feedback in the special app-feedback context | Manually create a TAPD ticket and include `APP反馈` when the source rule requires it. |
| Cloud classroom live class or replay issue | Route to Cloud Classroom 400 technical support; do not take over unless it is also a wider production incident. |
| Whitelist / permission opening in the group whose note says business teachers handle it | Do not process as duty tech issue; acknowledge and point to the business-side permission owner. |
| Student contact needed | Use the documented public WeCom support account; do not change account nickname/avatar; obtain verification code from the documented owner. Do not expose credentials in the answer. |
| Kaoyan app temporary/function group | Ask the group bot/assistant first; if unresolved, contact the mapped owner for app, backend/admin/image upload, or correction as relevant. |

When the group name is unclear because the source doc used screenshots, infer from text and ask for the exact group only if it changes the path.

## Severity Rules

Treat as emergency candidate when:

- Direct/live/recorded class flow fails.
- Order or payment flow fails.
- Course start/opening flow fails.
- Registration or login fails.
- The same issue gets 3 reports within 2 hours.

Emergency handling:

1. Acknowledge in the group quickly.
2. Collect minimal reproduction and impact details.
3. Contact emergency owners in order: QA, then developer, then PM.
4. Create or update TAPD and record current owner, impact, and next action.

For non-emergency unresolved issues, explain that it will be prioritized on the next workday, record the issue, and complete handoff.

## Minimum Evidence To Ask For

Ask for only the missing evidence needed to act:

- User role or account, if reproduction depends on identity.
- Page/module, action path, expected result, actual result.
- Screenshot or screen recording, if visual state matters.
- Time of occurrence and number of affected users.
- Order ID/course ID/class ID/payment info only when relevant; avoid unnecessary sensitive data.

## Closeout Checklist

At the end of duty, make sure every accepted issue has:

- Source group and reporter.
- Symptom and affected scope.
- TAPD link or note that no ticket was needed.
- Current owner and next step.
- Reporter sync status.
- Entry in the holiday duty table field `值班日技术工单list`.
- Duty group sync to the stability owner.

## Example Outputs

Input:
群：线下需求沟通问题处理群
反馈：老师说考研 App 词测图片上传失败，重试也不行。

Output:
处理结论：
- 这个要由值班人承接，走手工 TAPD。按 App 反馈类记录，工单标题或标签里补 `APP反馈`。

马上做：
1. 先在群里确认影响范围：是否单个老师、是否所有图片都失败、出现时间。
2. 收集截图、账号、操作路径、失败提示。
3. 手工录入 TAPD，指派给对应图片上传负责人，并把 TAPD 链接同步回群。

回复话术：
> 收到，我先记录为 App 反馈问题。麻烦补一下失败截图、操作账号、出现时间，以及是否所有图片都上传失败。我会同步建 TAPD 跟进，建好后把工单链接发群里。

工单/记录要点：
- 来源群：线下需求沟通问题处理群
- 问题现象：考研 App 词测图片上传失败
- 影响范围：待确认
- 处理动作：手工 TAPD，标注 APP反馈
- owner / 下一步：图片上传对应负责人排查
- 是否已同步反馈人：建单后同步

需要补充的信息：
- 失败截图、账号、时间、影响范围
