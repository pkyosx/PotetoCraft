# Measurement checklist

Use this whenever you produce a performance number: a before and after, a regression claim, or a choice between options. Answer each question with evidence from a run, not a guess from reading code.

For a quick ballpark the user asked for, one run is enough. Still answer questions 4 and 7, and say it was one run. A choice between options is never a ballpark.

Use only tools already on the machine or in the project. If a profiler or tool you want is missing, say so in the report and work with what exists.

## Before running

- Write the claim you expect to make, with numbers and units ("p50 export latency drops 30% on the 60k-row file"). The questions below test that sentence.
- Read the measurement script. Note what it times, what it counts, and what it skips.
- Check machine load with `uptime`. Check the core count with `nproc` on Linux or `sysctl -n hw.ncpu` on macOS. If the machine is busy and you cannot stop the load, alternate the runs so both sides see the same noise, and say so.

## Questions

1. **What limits it?** Name the bottleneck. Look at CPU per process (`top`, `ps`), I/O wait, and any profiler the language runtime already ships. Profile in a separate run, since profiling slows the work. If the load generator saturates first, you measured the load generator.
2. **Was each side configured like production?** Release builds, production flags, the same data, the same versions, caches as warm or cold as real use. If one side runs on defaults, you compared settings, not code. Fix the settings and measure again before naming a winner.
3. **Does it break a physical limit?** Do the arithmetic against disk and network bandwidth and core count. Removing a piece that takes 10% of the run can save at most about 10% of the time. A result past a limit means you measured a cache, a no-op, or a bug.
4. **Did anything fail?** Count errors and non-success responses. Check outputs are correct, not only present. Failures are often fast, and retries are slow.
5. **Does it repeat?** Run each side at least five times, alternating A and B. Report the median and the range. A gap smaller than the run-to-run spread is no measurable difference.
6. **Does it matter end to end?** Measure the path a user waits on, with realistic sizes and concurrency. Report a micro result as its share of that path.
7. **Did the work happen?** Confirm the timed region did the work. The request arrived, the rows were written, the result was used. Lazy values nobody reads and timeouts both produce fast, false numbers.

## Report

- Lead with the verdict: faster, slower, no measurable difference, or inconclusive.
- Give the number with its unit, the run count, the range, and the limiter. Example: "p50 41 ms to 33 ms, median of 7 runs per side, range 32 to 35 ms after, bound by JSON parsing on one core."
- Call it inconclusive when you cannot name the limiter, when a side ran untuned, or when you could not answer questions 4 and 7. Name the gap.
- Save the raw runs to a file in the scratch directory and give its path.
