# LINGYUN.Abp.TaskManagement.Domain.Shared

任务管理领域共享模块，包含共享的领域模型、枚举和常量。

## 功能

### 权限管理
- 任务调度平台权限
- 后台作业权限
- 作业行为权限
- 作业日志权限

### 作业类型和状态
- 作业类型:
  - 一次性作业（只执行一次）
  - 周期性作业（按照给定条件周期性运行）
  - 持续性作业（按照给定条件重复运行）
- 作业状态:
  - 未定义
  - 已完成
  - 运行中
  - 队列中
  - 已暂停
  - 失败重试
  - 已停止

### 优先级别
- 低
- 低于正常
- 正常
- 高于正常
- 高

### 作业属性
- 基本信息:
  - 分组
  - 名称
  - 描述
  - 类型
  - 状态
  - 开始/结束时间
- 执行设置:
  - 时间间隔（秒）
  - Cron表达式
  - 锁定超时时间
  - 优先级
  - 最大触发次数
  - 最大重试次数
- 跟踪信息:
  - 创建时间
  - 上次执行时间
  - 下次预期时间
  - 触发次数
  - 尝试次数
  - 执行结果

### 本地化
- 支持多语言
- 错误代码本地化
- UI文本本地化

### 多租户支持
- 租户级作业管理
- 系统级作业管理

### 来源类型
- 用户作业
- 系统内置作业
