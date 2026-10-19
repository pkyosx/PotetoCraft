# Measurement checklist

Run through this list before you report any timing, throughput, or resource number. That includes a single speedup claim, a suspected regression, and a choice between two designs. Every item is answered from a run you made, not from reading source.

Work with the profilers and timers already on the machine or in the project. If the one you want is absent, note that in the report and use what you have.

## How much rigor

| The number is for | Runs | Sections to answer |
|---|---|---|
| A rough sense of scale the user asked for | One, and the report says it was one | "Nothing failed" and "The work happened inside the timer" |
| A claim that something got faster or slower | Five or more per side | All of them |
| Picking one option over another | Five or more per side | All of them, with no shortcut |

A fast failure is wrong at any precision, which is why even a rough number gets the Real work checks.

## Set the target

Write the sentence you hope to report before you measure, with a unit. For example, "the CLI starts in under 3 s, down from 4.2 s." Then read the harness that produces the number. Note where its clock starts and stops and what falls outside that window.

## Fair fight

- **Same conditions on both sides.** Optimized build, real flags, identical input, identical dependency versions, and a cache state that matches real use. Ask whether the losing side would still lose after someone tuned it. If you cannot say, tune it, run again, and only then name a winner.
- **A quiet machine.** Look at `uptime` for load and at `nproc` (Linux) or `sysctl -n hw.ncpu` (macOS) for cores. If other work is running, leave it alone. Interleave the two sides so both absorb the same noise, and mention it.
- **Enough runs.** Interleave the sides, A, B, A, B. Report the median and the min to max range. A gap smaller than that range is no measurable difference.

## Real work

- **Nothing failed.** Count errors and non-success exits. Verify the outputs hold the right values. A request rejected by input validation can return a hundred times sooner than a real one, and that is not a speedup.
- **The work happened inside the timer.** The file was parsed, the rows were stored, the value was consumed. A lazy result nobody reads, or a timeout, gives a quick and meaningless time.
- **The math is possible.** Compare against disk speed, network bandwidth, and core count. If the download alone takes 2 s of a 3 s request, no parser change can bring that request below 2 s. A result past such a floor means a cache hit, skipped work, or a bug.

## Why this number

- **Find the limiter.** Watch per process CPU with `top` or `ps`, check I/O wait, and use the runtime's own profiler if it has one. Profile in a separate run, because profiling adds overhead. If the thing generating input maxes out first, the result describes that tool, not your code.
- **Place it in the whole.** Time what a user actually waits for, at realistic size and concurrency. Report a micro benchmark as a fraction of that.

## Report

Fill in these fields in this order:
- **Verdict.** Pick one word. Faster or slower when the gap clears the spread, "no measurable difference" when it does not, and inconclusive when a gap below applies.
- **Numbers.** Before and after, each with a unit, the run count per side, and the min to max range.
- **Limiter.** What held the number, and the profile or counter that showed it.
- **Gaps.** Anything above you could not answer. An unknown limiter, an untuned side, or a missing Real work check makes the verdict inconclusive.
- **Raw data.** The path of the file in the scratch directory that holds every run.
