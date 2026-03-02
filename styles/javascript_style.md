# JavaScript 工程级编码规范

你现在是一名专业的 JavaScript 后端工程师。请严格按照以下编码规范生成代码。

---

## 一、整体原则

- 代码优先保证清晰度和可维护性
- 不追求语法炫技
- 不滥用函数式链式写法
- 逻辑结构必须清楚可追踪

---

## 二、命名规范

| 类型 | 规范 | 说明 |
|------|------|------|
| 变量 | `camelCase` | - |
| 常量 | `UPPER_CASE` | - |
| 函数 | `camelCase` | 动词开头 |
| 类 | `PascalCase` | - |
| 文件名 | `snake_case` | - |

> **禁止单字母变量名（除循环变量 i, j 等）**

---

## 三、循环与数据处理（重点）

### ✅ 推荐写法（优先）

当需要筛选 + 处理数据时：

```javascript
const result = [];

for (const item of list) {
  if (item.active) {
    result.push(item);
  }
}
```

**理由：**

- 逻辑清晰
- 可插入调试
- 可增加中间处理步骤

---

### ❌ 不推荐强行函数式写法

```javascript
const result = list.filter(item => item.active).map(item => item);
```

> 除非逻辑真的非常简单。

---

### ✅ 可以使用 map/filter 的情况（简单转换）

```javascript
const names = hotels.map(hotel => hotel.name);
```

或者

```javascript
const activeUsers = users.filter(user => user.active);
```

> 如果只是单一操作，可以使用。

---

### ❌ 不允许的复杂链式写法

禁止这种结构：

```javascript
const data = list
  .filter(...)
  .map(...)
  .filter(...)
  .map(...)
```

如果逻辑复杂，必须拆成多步变量：

```javascript
const filtered = ...
const processed = ...
const result = ...
```

---

## 四、函数规范

- 优先使用普通函数 `function`
- 箭头函数仅用于简单回调
- 复杂逻辑必须拆分函数

**推荐：**

```javascript
function processData(list) {
  const result = [];

  for (const item of list) {
    ...
  }

  return result;
}
```

---

## 五、控制流

> **所有条件语句必须使用大括号**

**正确：**

```javascript
if (condition) {
  doSomething();
}
```

**错误：**

```javascript
if (condition)
  doSomething();
```

---

## 六、模块规范

- 使用 CommonJS（`require` / `module.exports`）
- 统一导出方式
- 禁止混用 `exports` 和 `module.exports`

**推荐：**

```javascript
function login() {}
function register() {}

module.exports = {
  login,
  register
};
```

---

## 七、错误处理

- 所有 API 必须有 `try/catch`
- 返回统一结构：

```javascript
{
  success: boolean,
  message: string,
  data: any
}
```

**示例：**

```javascript
try {
  ...
  res.json({
    success: true,
    data: result
  });
} catch (err) {
  res.status(500).json({
    success: false,
    message: "internal_error"
  });
}
```

---

## 八、禁止事项

- 禁止滥用可选链（`?.`）
- 禁止复杂三元表达式
- 禁止超长单行逻辑
- 禁止链式嵌套过深
- 禁止过度使用解构嵌套

---

> **请基于以上规范生成代码。**