# 新人入职 · 专属推广链接生成指南

## 一、问题与答案（FAQ）
### Q1：新人入职没有自己的 referral link，怎么生成？
**A**：使用公司国内 CRM 后台，通过固定链接替换参数即可生成专属推广链接。

### Q2：生成链接的规则是什么？
**A**：
- 基础链接：`https://crm.51suyang.cn/admin/test/test.php`
- 必须替换：`ids=111111111` → 改为**新人自己的 CRM ID**
- 岗位区分：
  - CC 岗位：`type=cc`（保持不变）
  - SS 岗位：`type=cc` → 改为 `type=is`

### Q3：访问后出现 `专属LandingPage已存在` 是什么意思？
**A**：该员工的专属落地页已经生成成功，**无需重复生成**，直接使用链接即可。

---

## 二、标准生成示例
### 1）CC 岗位示例
- 员工 CRM ID：`123456789`
- 生成链接：
```
https://crm.51suyang.cn/admin/test/test.php?ids=123456789&type=cc
```

### 2）SS 岗位示例
- 员工 CRM ID：`987654321`
- 生成链接：
```
https://crm.51suyang.cn/admin/test/test.php?ids=987654321&type=is
```

---

## 三、操作步骤
1. 登录国内 CRM 系统
2. 复制基础链接，替换 `ids` 为本人 CRM ID
3. 按岗位替换 `type` 参数（CC/IS）
4. 浏览器访问该链接
5. 提示`专属LandingPage已存在` → 生成完成

---

## 四、常见返回码说明
| 返回信息 | 含义 | 处理方式 |
|--------|------|----------|
| `专属LandingPage已存在` | 已生成成功 | 直接使用链接 |
| `参数错误` | ID/type 格式不对 | 检查ID是否纯数字、type是否cc/is |
| `无权限` | 未登录CRM | 先登录再访问 |
