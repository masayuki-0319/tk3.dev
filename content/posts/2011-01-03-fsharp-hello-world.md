---
title: F# で "Hello World"
date: 2011-01-03T23:14:01+09:00
slug: b8d9b109a162e68d47fa6f9c0b8724977373623a
---

F# で Hello World を出力。

```
#light

[<EntryPoint>]
let main (args : string[]) =
    printfn "Hello World"
    0
```
