load("//:openroad.bzl", "orfs_flow")

FAST_SETTINGS = {
    "REMOVE_ABC_BUFFERS": "1",
    "SKIP_REPORT_METRICS": "1",
    "SKIP_CTS_REPAIR_TIMING": "1",
    "SKIP_INCREMENTAL_REPAIR": "1",
}

orfs_flow(
    name = "sdq_17x64",
    abstract_stage = "grt",
    mock_area = 0.95,
    args = FAST_SETTINGS | {
        "SDC_FILE": "$(location //sram:fakeram/constraints-sram.sdc)",
        "CORE_UTILIZATION": "20",
        "CORE_MARGIN": "2",
        "MACRO_PLACE_HALO": "30 30",
        "PLACE_DENSITY": "0.25",
    },
    stage_sources = {
        "synth": ["//sram:fakeram/constraints-sram.sdc"],
    },
    verilog_files = ["//sram:fakeram/sdq_17x64.sv"],
)

orfs_flow(
    name = "top",
    abstract_stage = "grt",
    macros = ["//sram:sdq_17x64_generate_abstract"],
    args = FAST_SETTINGS | {
        "SDC_FILE": "$(location //sram:fakeram/constraints-sram.sdc)",
        "DIE_AREA": "0 0 100 100",
        "CORE_AREA": "2 2 98 98",
        "RTLMP_FLOW": "True",
        "CORE_MARGIN": "2",
        "MACRO_PLACE_HALO": "2 2",
    },
    stage_sources = {
        "synth": ["//sram:fakeram/constraints-sram.sdc"],
    },
    verilog_files = ["//sram:fakeram/top.v"],
)

# buildifier: disable=duplicated-name
orfs_flow(
    name = "top",
    variant="fakeram",
    abstract_stage = "grt",
    args = FAST_SETTINGS | {
        "SDC_FILE": "$(location //sram:fakeram/constraints-sram.sdc)",
        "DIE_AREA": "0 0 30 30",
        "CORE_AREA": "2 2 28 28",
        "RTLMP_FLOW": "True",
        "CORE_MARGIN": "2",
        "MACRO_PLACE_HALO": "2 2",
        "ADDITIONAL_LEFS": "$(location //sram:fakeram/sdq_17x64.lef)",
        "ADDITIONAL_LIBS": "$(location //sram:fakeram/sdq_17x64.lib)",
    },
    sources =  {
        "ADDITIONAL_LEFS" : ["//sram:fakeram/sdq_17x64.lef"],
        "ADDITIONAL_LIBS" : ["//sram:fakeram/sdq_17x64.lib"],
        "SDC_FILE": ["//sram:fakeram/constraints-sram.sdc"],
    },
    verilog_files = ["//sram:fakeram/top.v"],
)

# buildifier: disable=duplicated-name
orfs_flow(
    name = "sdq_17x64",
    variant = "megaboom",
    abstract_stage = "grt",
    mock_area = 0.95,
    args = FAST_SETTINGS | {
        "SDC_FILE": "$(location //sram:megaboom/constraints-sram.sdc)",
        "CORE_UTILIZATION": "20",
        "CORE_MARGIN": "2",
        "MACRO_PLACE_HALO": "30 30",
        "PLACE_DENSITY": "0.25",
    },
    stage_sources = {
        "synth": ["//sram:megaboom/constraints-sram.sdc"],
    },
    verilog_files = ["//sram:megaboom/sdq_17x64.sv"],
)

# buildifier: disable=duplicated-name
orfs_flow(
    name = "top",
    abstract_stage = "grt",
    variant = "megaboom",
    macros = ["//sram:sdq_17x64_megaboom_generate_abstract"],
    args = FAST_SETTINGS | {
        "SDC_FILE": "$(location //sram:megaboom/constraints-top.sdc)",
        "DIE_AREA": "0 0 100 100",
        "CORE_AREA": "2 2 98 98",
        "RTLMP_FLOW": "True",
        "CORE_MARGIN": "2",
        "MACRO_PLACE_HALO": "2 2",
    },
    stage_sources = {
        "synth": ["//sram:megaboom/constraints-top.sdc"],
    },
    verilog_files = ["//sram:megaboom/top.v"],
)
