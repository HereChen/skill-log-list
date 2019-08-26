# TypeScript

> <https://github.com/Microsoft/TypeScript>

```bash
npm install -g typescript
```

## Tips

* 生成声明文件: `tsc --declaration app.ts`
* 输入 `console.log` 时会自动添加 `console=require('console');`. 添加 `console.d.ts` 到 src 根目录. TODO: 貌似没用？

    ```javascript
    // https://github.com/microsoft/TypeScript/issues/30471
    // console.d.ts
    declare module 'console' {
        export = typeof import("console");
    }
    ```
