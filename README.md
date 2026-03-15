# MATLAB OnDemand App — KOA HPC Cluster

A BatchConnect app that runs MATLAB in your browser on the KOA HPC cluster. No local MATLAB install needed. Pick your resources, submit the job, and MATLAB opens in a new tab secured with token authentication.

## How it works

The app submits a SLURM job on the `mana` cluster. Inside that job, it loads the `matlab-proxy-app` module and starts a `matlab-proxy-app` server on an allocated port. OnDemand injects a one-time token (`MWI_AUTH_TOKEN`) so only you can access the session.

## Prerequisites

- Active account on KOA / UH HPC
- Access to the `tools/matlab` and `system/matlab-proxy` modules on the compute nodes
- OnDemand access at the cluster's web portal

## Setup

Clone into your OnDemand apps directory on the cluster:

```bash
git clone https://github.com/SammyCode002/matlab ~/ondemand/dev/matlab
```

Then open OnDemand, go to **My Interactive Sessions > My Sandbox Apps**, and the app will appear.

## Job form options

| Field | Description |
|---|---|
| SLURM Account | Leave blank if you only belong to one account |
| Queue | Partition to submit to |
| Hours | Wall time for the job |
| Cores | 1 to 40 cores per node |
| RAM (GB) | 1 to 1024 GB |
| GPU Type | Select from available GPU types on `mana` |
| GPU Count | 0 to 8 (0 means no GPU allocated) |
| Email on start | Get notified when the job begins |

## Notes

- MATLAB opens at `127.0.0.1` bound to the job's allocated port, proxied through OnDemand
- Token auth is handled by `MWI_ENABLE_TOKEN_AUTH=True` — the session password is set by OnDemand automatically
- If your cluster requires a license file, uncomment the `MATLAB_LICENSE_FILE` line in `template/script.sh.erb`

## License

MATLAB is a trademark of MathWorks, Inc. This app is not affiliated with MathWorks.
