# 会探AI events.json 增强字段说明

增强版数据保留原有字段，因此旧版小程序仍可正常读取。新增字段需要更新活动详情页后才会显示。

## 状态字段

- `status`: 程序使用的状态值。
  - `confirmed`: 官方已确认。
  - `pending_verification`: 待主办方确认。
  - `registration_closed`: 报名已截止。
  - `cancelled`: 活动取消。
- `statusText`: 给用户看的中文状态。
- `verifiedAt`: 最近核实日期，格式为 `YYYY-MM-DD`。
- `verificationNote`: 信息来源、已确认内容和仍需确认内容。

## 链接字段

- `infoUrl`: 活动介绍或信息发布页面。
- `registrationUrl`: 报名页面。暂时没有独立报名链接时，可与 `infoUrl` 相同。
- `url`: 兼容旧版小程序的链接，继续保留。

## 详情字段

- `organizer`: 主办方。
- `signupDeadline`: 报名截止时间；未知时为 `null`。
- `audience`: 适合人群。
- `highlights`: 活动亮点数组。
- `agenda`: 简要议程。
- `capacity`: 人数或名额；未知时为 `null`。
- `tags`: 标签数组。

## 更新规则

1. 官方页面确认日期、地点和主办方后，才将 `verified` 设为 `true`。
2. 只有聚合页时，使用 `pending_verification`，并在 `verificationNote` 中写明缺失信息。
3. 不猜测费用、名额或报名截止时间；未知值使用 `null`。
4. 活动结束、取消或信息冲突且无法确认时，从公开列表移除。
5. 更新时间后同时修改顶层 `updatedAt` 和每场活动的 `verifiedAt`。

## 微信小程序链接建议

活动详情页优先展示 `infoUrl` 和 `registrationUrl`。如果外部域名未配置为微信小程序业务域名，点击按钮时复制链接，并提示用户在浏览器打开；这样可以兼容不同活动平台。
