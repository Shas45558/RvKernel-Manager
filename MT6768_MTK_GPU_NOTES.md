# MT6768 MTK GPU support

This build adds MediaTek GED GPU detection and parsing for the MT6768 GED interface.

Supported read nodes:
- `/sys/kernel/ged/hal/current_freqency`
- `/sys/kernel/ged/hal/opp_logs`
- `/sys/kernel/ged/hal/gpu_utilization`

The OPP table is parsed without dropping the first entry, so a table containing
950000000 ... 299000000 is displayed as 950 MHz ... 299 MHz.

## GPU max-frequency control

Some MediaTek GED kernels expose a writable `custom_upbound_gpu_freq` node. The
app checks these locations through the root shell:

- `/sys/kernel/ged/hal/custom_upbound_gpu_freq`
- `/sys/kernel/debug/ged/hal/custom_upbound_gpu_freq`
- `/d/ged/hal/custom_upbound_gpu_freq`

That node expects the OPP index, not MHz. The app converts the selected frequency
to the corresponding OPP index before writing it.

## GPU minimum frequency

The MT6768 interface used by this device exposes no true minimum-frequency floor
node in the observed GED interface. `custom_boost_gpu_freq` is not treated as a
fake minimum because it is a boost control, not an equivalent min-frequency
limit. Therefore the Min freq control remains disabled on MTK when no genuine
minimum control is available.
