# SQL 月度分表工具

一个用于快速生成 SQL 分表语句的在线工具，支持将一个大表的查询按月份分段拆分为多个小表。

## 功能特点

- 📅 **月份选择** - 支持快速切换目标月份，带有 +/- 按钮
- 🔄 **自动检测** - 自动从原始 SQL 中提取 MONTH_ID、日期字段等
- ⚙️ **分段配置** - 可自定义每个表的日期范围，支持添加/删除分段
- 🎨 **可视化预览** - 实时预览生成结果，高亮显示替换内容
- 📋 **一键复制** - 支持单独复制或批量复制所有 SQL

## 使用方法

### 1. 配置基本信息

- **表名前缀**：填写要生成的表名前缀（如 `HB_SERVICE_REQUEST`）
- **目标月份**：选择目标月份（默认当前月）

### 2. 粘贴原始 SQL

将需要分表的原始 SQL 语句粘贴到文本框中，例如：

```sql
CREATE TABLE selfhelp.HB_SERVICE_REQUEST_202511_01_08 AS
SELECT 
    a.DAY_ID,
    a.CONTACT_ID,
    a.CODE_CONTACT_CHANNEL,
    a.CODE_CONTACT_DIRECTION
FROM ALLDM.DWD_D_EVT_KF_JC_MANUAL_SEAT a
WHERE 
    MONTH_ID = '202511'
    AND CREATE_TIME >= '2025-11-01 00:00:00'
    AND CREATE_TIME <= '2025-11-08 23:59:59'
    AND CODE_CONTACT_DIRECTION = '01'
```

### 3. 配置分段日期

工具会自动将一个月分成 4 个时间段：

- 第1段：01日 ~ 08日
- 第2段：09日 ~ 17日
- 第3段：18日 ~ 25日
- 第4段：26日 ~ 31日

可以根据需要调整每个分段的日期范围，也可以添加或删除分段。

### 4. 生成 SQL

点击「生成SQL」按钮，工具会：

- 自动替换表名中的月份和日期范围
- 自动替换 MONTH_ID
- 自动替换日期条件
- 生成 4 个（或自定义分段数量）的 SQL 语句

### 5. 复制使用

- 点击单个 SQL 的「复制此SQL」按钮复制对应的 SQL
- 点击「复制全部」按钮复制所有 SQL

## 替换规则

工具会自动处理以下替换：

| 替换项 | 说明 |
|--------|------|
| 表名 | `HB_SERVICE_REQUEST_202511_01_08` → `HB_SERVICE_REQUEST_202512_01_08` |
| MONTH_ID | `202511` → `202512` |
| 日期范围 | 根据分段配置自动替换 |

## 在线访问

访问地址：https://hbpc002.github.io/sql-monthly-splitter/

## 技术栈

- 纯 HTML + CSS + JavaScript
- 无需后端，纯前端处理
- 响应式设计，支持移动端

## 适用场景

- 月度数据归档
- 大表拆分
- 历史数据迁移
- 报表数据准备
