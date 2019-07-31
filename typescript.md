# TypeScript

## Tips

* 输入 `console.log` 时会自动添加 `console=require('console');`. 添加 `console.d.ts` 到 src 根目录.

    ```javascript
    // https://github.com/microsoft/TypeScript/issues/30471
    // console.d.ts
    declare module 'console' {
        export = typeof import("console");
    }
    ```
