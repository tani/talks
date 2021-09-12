---
marp: true
theme: default
---


![bg left:25% 100%](https://upload.wikimedia.org/wikipedia/commons/8/84/Deno.svg)

# Import Maps and Search Parameters <br> :: sky.deno.dev


GitHub: https://github.com/tani
Webpage: https://docs.casa

https://talks.docs.casa/denobata01

---
## Code

```ts
self.addEventListener("fetch", (event) => {
  let dest = "https://github.com/tani/sky.deno.dev";
  const url = new URL(event.request.url)
  if (url.pathname !== "/") {
    url.host = "cdn.skypack.dev"
    url.searchParams.set("dts", "")
  }
  event.respondWith(Response.redirect(url, 302));
});
```

---
## Import Maps

仕様 (Draft): https://wicg.github.io/import-maps/

---
## Search Parameters

仕様 (WHATWG): https://url.spec.whatwg.org/#dom-urlsearchparams-urlsearchparams

---

## Skypack

https://www.skypack.dev

---
## sky.deno.dev
各ファイルごとにImport Mapsを用意しなくても良くなり，スッキリする
```diff
{   
-    "foo": "https://cdn.skypack.dev/foo@1.0.0?dts",
-    "util": "https://cdn.skypack.dev/foo@1.0.0/util.js?dts"
+    "foo": "https://sky.deno.dev/foo@1.0.0"
}
```
```diff
  import foo from "foo"
- import util from "util"
+ import util from "foo/util"
```

---
## 関連プロジェクト lib.deno.dev

- Toranoana.deno#1で話す予定
- deno.land 用のセマンティックバージョンニング拡張

```ts
import foo from "https://lib.deno.dev@v1.x"
```

---
## Deno Deploy x Deno import

- On-the-flyで変換するプロキシーを作るのもよし
- 302リダイレクトでリクエストを書き換えるのもよし
- 実行時間制限とメモリ制限があることに注意！

---

![bg right:25% 100%](https://upload.wikimedia.org/wikipedia/commons/8/84/Deno.svg)

## Thanks