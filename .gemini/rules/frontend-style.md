# 前端开发规范（补充）

> 补充 GEMINI.md 和 frontend-safety skill 未覆盖的前端规范。
> UI 风格约束见 GEMINI.md，布局/覆盖层规范见 skills/frontend-safety/。

---

## 1. 状态管理（Pinia）

### Store 定义

使用 Composition API 风格（`setup` 函数）定义 Store：

```typescript
// stores/user.ts
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'
import type { User } from '@/types'

export const useUserStore = defineStore('user', () => {
  const user = ref<User | null>(null)
  const token = ref<string>('')

  const isLoggedIn = computed(() => !!token.value)

  async function login(username: string, password: string) {
    const res = await api.login(username, password)
    token.value = res.token
    user.value = res.user
  }

  function logout() {
    token.value = ''
    user.value = null
  }

  return { user, token, isLoggedIn, login, logout }
})
```

### 在组件中使用

```typescript
import { useUserStore } from '@/stores/user'
import { storeToRefs } from 'pinia'

const userStore = useUserStore()

// ✅ 使用 storeToRefs 保持响应性
const { user, isLoggedIn } = storeToRefs(userStore)

// ✅ actions 直接解构
const { login, logout } = userStore
```

---

## 2. API 请求规范

### 模块组织

```
src/api/
├── index.ts        # 统一导出
├── user.ts         # 用户相关
└── product.ts      # 商品相关
```

### 请求封装要点

| 要点 | 说明 |
|------|------|
| 统一 baseURL | 从 `import.meta.env.VITE_API_BASE_URL` 读取 |
| 请求拦截 | 自动附加 `Authorization: Bearer <token>` |
| 响应拦截 | 统一处理错误码，`ElMessage.error` 提示 |
| 超时设置 | 默认 10s |

### API 请求一致性规范

- **拦截器解包对齐**：若项目 `request.ts` 存在自动解包拦截器（如 `return res.data`），则 API 定义中的 Promise 泛型**必须直接对应解包后的数据类型**（如 `Promise<User[]>`），严禁将包装类 `ApiResponse<T>` 赋值给业务变量。
- **工具链补齐**：业务若需 `PATCH` 等方法而 `request.ts` 未导出对应包装函数，**必须先补齐工具类定义**，严禁在 API 层使用 `(request.get as any)` 等强转手段。

---

## 3. TypeScript 规范

| 规则 | 说明 |
|------|------|
| 禁止大范围 `any` | 必须为 API 响应定义类型 |
| Props/Emits 必须类型定义 | 使用泛型式 `defineProps<{...}>()` |
| 类型文件放 `types/` 目录 | 按模块拆分（`user.ts`、`api.ts`） |

```typescript
// types/api.ts
export interface ApiResponse<T = unknown> {
  code: number
  message: string
  data: T
}

export interface PageResult<T> {
  list: T[]
  total: number
}
```

---

## 4. 交互状态规范

所有数据展示页面必须处理以下状态：

| 状态 | 说明 | 组件 |
|------|------|------|
| loading | 加载中 | `<el-skeleton>` |
| empty | 空数据 | `<el-empty>` |
| error | 错误 | `<el-result icon="error">` + 重试按钮 |
| submitting | 提交中 | 按钮 `loading` + 防重复点击 |

---

## 5. 性能优化要点

| 场景 | 方案 |
|------|------|
| 大列表 | 虚拟滚动（`el-table-v2`） |
| 搜索输入 | 防抖 300ms（`useDebounceFn`） |
| 路由/组件 | 懒加载（`() => import(...)` / `defineAsyncComponent`） |
| 大数据 | `shallowRef` 替代 `ref` |
| 静态内容 | `v-once` 标记 |
| 打包 | 分包（vendor/element-plus 独立 chunk） |
