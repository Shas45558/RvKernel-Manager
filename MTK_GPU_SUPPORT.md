# MediaTek GPU support

This version adds MediaTek GED/GPUFREQ detection for kernels exposing:

- `/sys/kernel/ged/hal/current_freqency`
- `/sys/kernel/ged/hal/opp_logs`
- `/sys/kernel/ged/hal/gpu_utilization`

For the tested MT6768 interface, `current_freqency` is parsed as `OPP_INDEX FREQUENCY_KHZ`, and `opp_logs` is parsed as the GPU OPP table in Hz. Frequencies are displayed in MHz.

Qualcomm KGSL support remains unchanged.

For MTK GED kernels, min/max frequency controls and the governor selector are disabled because the detected interface is a statistics/DVFS interface rather than a standard writable KGSL/devfreq interface. This prevents the app from accidentally writing to a read-only GED statistics file.

## Build note

The source was checked for the intended changes. A local Gradle APK build could not be completed in the build environment because the Gradle wrapper distribution was not cached and external network access was unavailable.
