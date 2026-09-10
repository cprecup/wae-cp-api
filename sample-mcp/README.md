# RPC and OPM-based script

## Introduction
This sample script is intended to simulate an MCP Server for Cisco Crosswork Planning.
This script uses the CP Python API libraries and must be run from a Linux instance with the CP SDK installed.
Please notice that the following details are set as global variables in this script:
- CP server host
- CP opm service port
- CP opm service protocol
- Plan file

# Tools
Consult the documentation for each script in the sample-scripts folder to see its functionality in detail.

    - get_worst_case_traffic_utilization()
    - run_specific_failure_simulation()
    - get_route_shortest_path()

## Run the script from the CP SDK Client
Notice that any required input file (plan file or others) in this example has been previously uploaded / imported into the SDK client.

    uv init cp-agent-server
    cd cp-agent-server
    uv venv
    source .venv/bin/activate
    uv pip install -r requirements.txt
    nano .env # Update with your own token, CARIDEN_HOME, and CP_* values
    uv run cp-agent-server-http.py

The Design/OPM Python APIs (`com.cisco.wae`) come from the CP SDK on the host, not from PyPI. Set `CARIDEN_HOME` in `.env` to the `cw-planning` directory (the one that contains `lib/python/com/cisco/wae`). See `.env.example`.

Set `CP_HOST`, `CP_PORT`, `CP_PROTOCOL`, `CP_PLAN_FILE_NAME`, and `CP_PLAN_FILE` in `.env` to your Crosswork Planning server and plan file. The values in the script and `.env.example` are placeholders.

To run under systemd, copy `cp-agent-server.service` to `/etc/systemd/system/`, edit the paths for this host, then `daemon-reload` and `enable --now`.

## Query examples:

    1. Please do the evaluation of failures in all circuits and nodes in the network, and tell me what would be the maximum interface utilization and the interface name
    2. If node cr1.wdc fails, what would be the maximum interface utilization in my network
    3. I need to add a new demand from node er1.sea to node er1.mia with 1G of traffic, and need to know if there is enough capacity, and what would be the maximum interface utilization