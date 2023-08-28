# Bestest TypeScript runner in Node

This is the sample code used for this blog post:
[**ts-node vs. esrun vs. esno vs. bun**](https://www.peterbe.com/plog/ts-node-vs-esrun-vs-esno-vs-bun)

## Install

```sh
npm i -D typescript ts-node esno @digitak/esrun
```

## Run options

1. `tsc`

    tsc src/index.ts && node src/index.js

1. `ts-node`

    ts-node src/index.ts

1. `ts-node --transpileOnly`

    ts-node --transpileOnly src/index.ts

1. `esrun`

    esrun src/index.ts

1. `esno`

    esno src/index.ts

1. `bun`

    bun src/index.ts

## Hyperfine

Run:

```sh
hyperfine "tsc src/index.ts && node src/index.js" "ts-node src/index.ts" "ts-node --transpileOnly src/index.ts" "esrun src/index.ts" "esno src/index.ts" "bun src/index.ts"
```

### Result

```sh
Benchmark 1: tsc src/index.ts && node src/index.js
  Time (mean ± σ):      2.360 s ±  0.095 s    [User: 5.651 s, System: 0.205 s]
  Range (min … max):    2.225 s …  2.474 s    10 runs

Benchmark 2: ts-node src/index.ts
  Time (mean ± σ):     997.5 ms ±   5.5 ms    [User: 2007.7 ms, System: 119.0 ms]
  Range (min … max):   989.9 ms … 1006.4 ms    10 runs

Benchmark 3: ts-node --transpileOnly src/index.ts
  Time (mean ± σ):     306.3 ms ±   2.5 ms    [User: 295.4 ms, System: 44.4 ms]
  Range (min … max):   303.5 ms … 312.0 ms    10 runs

Benchmark 4: esrun src/index.ts
  Time (mean ± σ):     235.8 ms ±   1.3 ms    [User: 198.7 ms, System: 43.5 ms]
  Range (min … max):   234.3 ms … 238.1 ms    12 runs

Benchmark 5: esno src/index.ts
  Time (mean ± σ):     248.3 ms ±   2.8 ms    [User: 236.3 ms, System: 45.3 ms]
  Range (min … max):   243.2 ms … 252.8 ms    11 runs

Benchmark 6: bun src/index.ts
  Time (mean ± σ):      41.2 ms ±   0.8 ms    [User: 30.4 ms, System: 10.0 ms]
  Range (min … max):    38.9 ms …  43.6 ms    62 runs

Summary
  bun src/index.ts ran
    5.73 ± 0.12 times faster than esrun src/index.ts
    6.03 ± 0.14 times faster than esno src/index.ts
    7.44 ± 0.16 times faster than ts-node --transpileOnly src/index.ts
   24.22 ± 0.50 times faster than ts-node src/index.ts
   57.31 ± 2.57 times faster than tsc src/index.ts && node src/index.js
```
