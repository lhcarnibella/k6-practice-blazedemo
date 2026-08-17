# K6 Practice — BlazeDemo

First hands-on practice with K6 (load testing), covering fixed VUs, ramping VUs (stages), and a basic stress test, against BlazeDemo (a public demo site by BlazeMeter).

## Status

This is an introductory practice project — first contact with K6 fundamentals (Virtual Users, thresholds, stages). It covers the core mechanics but not deep performance analysis. A more thorough practice project (with a richer target application and more complete scenarios) is planned as a follow-up.

## What's covered

- **`tests/fixed-vus-test.js`** — basic load test with a fixed number of VUs
- **`tests/ramping-vus-test.js`** — load test using `stages` to simulate gradual user ramp-up/ramp-down
- **`tests/stress-test.js`** — stress test with progressively increasing VU steps (kept to a moderate max of 30 VUs, out of respect for a shared public demo resource)

## Key findings

- BlazeDemo showed no measurable performance degradation up to 30 concurrent VUs (p(95) stayed around ~320ms across all three scripts) — no breaking point was found within a responsible load range against a public demo site.
- Thresholds (`p(95)<400ms` for load tests, `p(95)<800ms` for the stress test; error rate thresholds) were defined based on an initial baseline run, not a real business SLA — this is an explicit limitation, since no such SLA exists for a public demo site. In a real project, thresholds should come from a documented SLA, historical monitoring baseline, or a before/after comparison — not an arbitrary number.

## Setup

```bash
npm init -y
npm install --save-dev @types/k6   # optional, editor type support only
```

Requires K6 installed locally (`winget install k6` on Windows).

## Running

```bash
k6 run tests/fixed-vus-test.js
k6 run tests/ramping-vus-test.js
k6 run tests/stress-test.js
```
