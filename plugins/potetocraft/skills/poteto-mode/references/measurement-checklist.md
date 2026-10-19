# Measurement checklist

Run through this list before you report any timing, throughput, or resource number. That includes a single speedup claim, a suspected regression, and a choice between two designs. Every item is answered from a run you made, not from reading source.

Work with the profilers and timers already on the machine or in the project. If the one you want is absent, note that in the report and use what you have.

## Set the target

Write the sentence you hope to report before you measure, with a unit. For example, "the CLI starts in under 3 s, down from 4.2 s." Then read the harness that produces the number. Note where its clock starts and stops and what falls outside that window.

## Fair fight

- **Same conditions on both sides.** Optimized build, real flags, identical input, identical dependency versions, and a cache state that matches real use. If one side ran with defaults, you compared settings, not code. Correct it and rerun before you pick a winner.
- **A quiet machine.** Look at `uptime` for load and at `nproc` (Linux) or `sysctl -n hw.ncpu` (macOS) for cores. If other work is running, leave it alone. Interleave the two sides so both absorb the same noise, and mention it.
- **Enough runs.** Five or more per side, interleaved A, B, A, B. Report the median and the min to max range. A gap smaller than that range is no measurable difference.

## Real work

- **Nothing failed.** Count errors and non-success exits. Verify the outputs hold the right values. A crash is often quick, and a retry is often slow.
- **The work happened inside the timer.** The file was parsed, the rows were stored, the value was consumed. A lazy result nobody reads, or a timeout, gives a quick and meaningless time.
- **The math is possible.** Compare against disk speed, network bandwidth, and core count. Removing a step that costs 10% of the run cannot save much more than 10%. A result past that bound means a cache hit, skipped work, or a bug.

## Why this number

- **Find the limiter.** Watch per process CPU with `top` or `ps`, check I/O wait, and use the runtime's own profiler if it has one. Profile in a separate run, because profiling adds overhead. If the thing generating input maxes out first, the result describes that tool, not your code.
- **Place it in the whole.** Time what a user actually waits for, at realistic size and concurrency. Report a micro benchmark as a fraction of that.

## Quick estimates

If the user asks only for a ballpark, one run is enough. You still answer the two Real work items about failures and work inside the timer, and you say that only one run was made. Choosing between options always needs the full list.

## Report

- Start with the verdict. Choose among faster, slower, inconclusive, and no measurable difference.
- Give the value with its unit, run count, spread, and limiter. For instance, "cold start went from 4.2 s to 2.8 s, 9 runs each, 2.7 to 3.0 s after, limited by config file parsing."
- Mark it inconclusive when the limiter is unknown, a side was not configured fairly, or a Real work item is unanswered. Name the gap.
- Write the raw run data to a file in the scratch directory and give the path.
