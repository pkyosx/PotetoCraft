# Measurement checklist

Use this whenever you produce a performance number: a before and after, a regression claim, or a choice between options. Every answer must come from something you ran, never from reading code and guessing.

When the user only wants a rough estimate, a single run will do. Questions 4 and 7 still need answers, and the report must mention that only one run happened. Comparing options always needs the full procedure.

Use only tools already on the machine or in the project. If a profiler or tool you want is missing, say so in the report and work with what exists.

## Before running

- Write the claim you expect to make, with numbers and units ("p50 export latency drops 30% on the 60k-row file"). The questions below test that sentence.
- Read the benchmark code. Write down which region it times, which events it counts, and what it leaves out.
- Check machine load with `uptime`. Check the core count with `nproc` on Linux or `sysctl -n hw.ncpu` on macOS. If the machine is busy, do not stop or kill anything you did not start. Alternate the runs so both sides see the same noise, and say so.

## Questions

1. **What limits it?** Name the bottleneck. Look at CPU per process (`top`, `ps`), I/O wait, and any profiler the language runtime already ships. Profile in a separate run, since profiling slows the work. If the load generator saturates first, you measured the load generator.
2. **Was each side configured like production?** Release builds, production flags, the same data, the same versions, caches as warm or cold as real use. A side left on default settings turns the result into a test of configuration, not of the change. Fix the settings and measure again before naming a winner.
3. **Does it break a physical limit?** Do the arithmetic against disk and network bandwidth and core count. Cutting a step worth 10% of the total cannot speed the whole thing up by much more than 10%. Any result beyond such a limit points to caching, work that never ran, or a defect.
4. **Did anything fail?** Count errors and non-success responses. Check outputs are correct, not only present. Failures are often fast, and retries are slow.
5. **Does it repeat?** Run each side at least five times, alternating A and B. Report the median and the range. When the difference sits inside the normal variation between runs, call it no measurable difference.
6. **Does it matter end to end?** Measure the path a user waits on, with realistic sizes and concurrency. Report a micro result as its share of that path.
7. **Did the work happen?** Confirm the timed region did the work. The request arrived, the rows were written, the result was used. Lazy values nobody reads and timeouts both produce fast, false numbers.

## Report

- Open with one of four verdicts: faster, slower, no measurable difference, or inconclusive.
- State the number and its unit, how many runs, the spread, and what limits it. Example: "p95 import time fell from 2.4 s to 1.9 s over 9 runs per side. After the change it ranged 1.8 to 2.0 s, limited by disk reads."
- The verdict is inconclusive if the limiter is unknown, if either side was not tuned, or if question 4 or 7 has no answer. Say which piece is missing.
- Save the raw runs to a file in the scratch directory and give its path.
