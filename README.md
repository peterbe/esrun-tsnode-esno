# Bestest TypeScript runner in Node

This is the sample code used for this blog post:
[**ts-node vs. esrun vs. esno vs. bun**](https://www.peterbe.com/plog/ts-node-vs-esrun-vs-esno-vs-bun)

## Install

```sh
npm i -D typescript ts-node esno esrun tsx
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

1. `tsx`

    tsx src/index.ts

## Hyperfine

Run:

```sh
hyperfine "tsc src/index.ts && node src/index.js" "ts-node src/index.ts" "ts-node --transpileOnly src/index.ts" "esrun src/index.ts" "esno src/index.ts" "bun src/index.ts" "tsx src/index.ts"
```

### Result

```sh
Benchmark 1: tsc src/index.ts && node src/index.js
  Time (mean ± σ):      1.867 s ±  0.069 s    [User: 4.374 s, System: 0.157 s]
  Range (min … max):    1.714 s …  1.983 s    10 runs

Benchmark 2: ts-node src/index.ts
  Time (mean ± σ):     944.2 ms ±  26.2 ms    [User: 1974.5 ms, System: 126.0 ms]
  Range (min … max):   900.5 ms … 984.0 ms    10 runs

Benchmark 3: ts-node --transpileOnly src/index.ts
  Time (mean ± σ):     292.0 ms ±   8.0 ms    [User: 272.4 ms, System: 47.2 ms]
  Range (min … max):   281.4 ms … 303.3 ms    10 runs

Benchmark 4: esrun src/index.ts
  Time (mean ± σ):     184.7 ms ±   3.5 ms    [User: 157.2 ms, System: 34.5 ms]
  Range (min … max):   177.1 ms … 189.6 ms    15 runs

Benchmark 5: esno src/index.ts
  Time (mean ± σ):     285.9 ms ±   8.1 ms    [User: 270.4 ms, System: 46.4 ms]
  Range (min … max):   272.6 ms … 293.5 ms    10 runs

Benchmark 6: bun src/index.ts
  Time (mean ± σ):      40.3 ms ±   1.1 ms    [User: 28.7 ms, System: 12.1 ms]
  Range (min … max):    37.2 ms …  43.9 ms    61 runs

Benchmark 7: tsx src/index.ts
  Time (mean ± σ):     277.2 ms ±   9.1 ms    [User: 265.1 ms, System: 45.0 ms]
  Range (min … max):   266.2 ms … 292.6 ms    10 runs

Summary
  bun src/index.ts ran
    4.58 ± 0.15 times faster than esrun src/index.ts
    6.88 ± 0.29 times faster than tsx src/index.ts
    7.10 ± 0.28 times faster than esno src/index.ts
    7.25 ± 0.28 times faster than ts-node --transpileOnly src/index.ts
   23.43 ± 0.90 times faster than ts-node src/index.ts
   46.33 ± 2.11 times faster than tsc src/index.ts && node src/index.js
```

Considering how significantly slower `tsc src/index.ts && node src/index.js`
and `ts-node src/index.ts` are, because they write a `index.js`  file to
disk every time, here's a benchmark with them skipped:

```sh
hyperfine "ts-node --transpileOnly src/index.ts" "esrun src/index.ts" "esno src/index.ts" "bun src/index.ts" "tsx src/index.ts"
```

```sh
Benchmark 1: ts-node --transpileOnly src/index.ts
  Time (mean ± σ):     305.3 ms ±  27.3 ms    [User: 278.9 ms, System: 51.7 ms]
  Range (min … max):   283.7 ms … 380.8 ms    10 runs

  Warning: Statistical outliers were detected. Consider re-running this benchmark on a quiet system without any interferences from other programs. It might help to use the '--warmup' or '--prepare' options.

Benchmark 2: esrun src/index.ts
  Time (mean ± σ):     193.6 ms ±   7.0 ms    [User: 164.0 ms, System: 35.6 ms]
  Range (min … max):   183.4 ms … 206.6 ms    15 runs

Benchmark 3: esno src/index.ts
  Time (mean ± σ):     298.6 ms ±  11.8 ms    [User: 286.8 ms, System: 50.1 ms]
  Range (min … max):   285.7 ms … 325.0 ms    10 runs

Benchmark 4: bun src/index.ts
  Time (mean ± σ):      41.3 ms ±   1.0 ms    [User: 28.9 ms, System: 12.6 ms]
  Range (min … max):    39.8 ms …  44.7 ms    59 runs

Benchmark 5: tsx src/index.ts
  Time (mean ± σ):     291.6 ms ±  10.1 ms    [User: 278.4 ms, System: 47.5 ms]
  Range (min … max):   272.4 ms … 311.3 ms    10 runs

Summary
  bun src/index.ts ran
    4.69 ± 0.20 times faster than esrun src/index.ts
    7.07 ± 0.30 times faster than tsx src/index.ts
    7.24 ± 0.33 times faster than esno src/index.ts
    7.40 ± 0.68 times faster than ts-node --transpileOnly src/index.ts
```
