# Ratatouille

[![DOI](https://zenodo.org/badge/173307160.svg)](https://zenodo.org/badge/latestdoi/173307160)

## Local Installation

```
curl -sSL https://install.python-poetry.org | python3 -
poetry install ratatouille
```

For NVIDIA GPUs monitoring install the python bindings for the NVIDIA Management Library (NVML) - C-based.

```
python3 -m pip install nvidia-ml-py
```

Use other configuration file for newer python versions.

To reinstall:

```
pip uninstall ratatouille
/home/ana/.local/bin/poetry build
pip install dist/ratatouille-0.1.0-py3-none-any.whl --force-reinstall
```

If error, try to clean the cache:

```
/home/ana/.local/bin/poetry list
# For example:
/home/ana/.local/bin/poetry cache clear  PyPI --all
```

## Installation

The best way to install `ratatouille` is from pypi:
```sh
pip install ratatouille
```

Alternatively, you can install from `master` as follows:
```sh
pip install git+https://github.com/Ezibenroc/ratatouille.git
```

## Example of usage

Collect data in file `/tmp/data.csv` with a 3 seconds interval (press Ctr-C to stop).
```sh
ratatouille collect -t 3 all /tmp/data.csv
```

Collect only the temperature and frequency:
```sh
ratatouille collect -t 3 cpu_freq temperature /tmp/data.csv
```

Plot the data stored in file `/tmp/data.csv`.
```sh
ratatouille plot /tmp/data.csv
```

For this last command, you need to install extra dependencies:
```sh
pip install pandas plotnine
```

## Collected data

When collecting data you can either collect all data (with the `all` target argument) or a subset of the data:

- `cpu_freq` collects the frequency (in `Hertz`) of each *logical* CPU core listed in `/sys/devices/system/cpu/`.
- `cpu_load` collects the percentage load of the CPUs.
- `cpu_power` computes the average power consumption (in `Watts`) of each package listed in `/sys/devices/virtual/powercap/intel-rapl/` between two intervals. Additional values for the `core`, `uncore` and `dram` are also collected if available.
- `cpu_stats` collects the total number of context switches, interrupts and soft_interrupts since boot.
- `fan_speed` collects the rotation speed of fans.
- `memory_usage` collects the current memory available (in bytes) and its percentage over the total memory.
- `network` collects the total number of bytes sent and received on each network interface.
- `temperature` collects the temperature (in Celsius or Farenheit degrees, depending on your configuration) of each *physical* CPU core and other thermal sensors.

Notice that `cpu_load`, `cpu_stats`, `fan_speed`, `memory_usage`, `network` and `temperature` rely on [psutil](https://github.com/giampaolo/psutil) to collect data.
