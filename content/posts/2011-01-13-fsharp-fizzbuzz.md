---
title: F# で Fizz Buzz
date: 2011-01-13T00:00:00+09:00
slug: 62967a6911d254608b5a37857c4500560906f721
---

何となく F# っぽさが足りないように思えたけれど、今の実力ではこれが精一杯。

```
#light

let FizzBuzz n =
    let rec loop n l =
        match n with
        | 0 -> l
        | x when x % 3 = 0 && x % 5 = 0 -> loop (n - 1) ["Fizz Buzz"] @ l
        | x when x % 3 = 0              -> loop (n - 1) ["Fizz"] @ l
        | x when x % 5 = 0              -> loop (n - 1) ["Buzz"] @ l
        | x                             -> loop (n - 1) [sprintf "%d" x] @ l
    loop n []

[<EntryPoint>]
let main (args : string[]) =
    let result = FizzBuzz 100
    printfn "%A" result
    0
```
