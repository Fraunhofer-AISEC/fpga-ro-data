# Measurement Data for "Large Scale RO PUF Analysis over Slice Type, Evaluation Time and Temperature on 28nm Xilinx FPGAs"

This repository contains the ring oscillator frequencies gathered from 217 Xilinx
Artix7 devices (Part#: XC7A35T-1CPG236C) that were analyzed in and published
with the paper "Large Scale RO PUF Analysis over Slice Type, Evaluation Time
and Temperature on 28nm Xilinx FPGAs" at HOST 2018.

To download the entire repository as a .ZIP file click the green "Clone or download"-Butten on the top right of this page and click on "Download ZIP".

The repository is organized as follows:

## Directory structure
The actual measurement data is located in the directories

+ `ro_frequency_temperature/`
+ `ro_frequency_evaluation_time/`

They each contain 4 files named:

* `LEFT-LOWER.hdf5`
* `LEFT-UPPER.hdf5`
* `RIGHT-LOWER.hdf5`
* `RIGHT-UPPER.hdf5`

Each file corresponds to one measurement run with one of the 4 different bitstreams/fpga-configurations described in the paper.

### `ro_frequency_temperature/`
measured on 50 FPGAs at ambient temperatures 5 °C, 15 °C, 25 °C, 35 °C, 45 °C, 55 °C

### `ro_frequency_evaluation_time/`
measured on 217 FPGAs at ambient room temperature

### `placement_information/`
detailed info on placement for each bitstream in csv format


## HDF5 structure (ro_ids size depends on design)

### `axis/`
Contains axis datasets:

* `board_serialnumbers`
* `evaluation_times`
* `repetitions`
* `ro_ids`
* `temperatures`

These are linked to the dimensions of the actual dataset data/ro_counts and map the indexes of a dimension to a value.
For example `axis/temperature` is linked to the dimension with the index 2 of `data/ro_counts`, which means that all values `data/ro_counts[:,:,i,:,:]` correspond to the temperature `axis/temperature[i]`.

`evaluation_times` is the number of system clock cycles that were counted at **100MHz** before the RO counter was stopped.

### `data/`
contains the actual ro frequency dataset:
	`data/ro_counts`.  
It contains the raw counter values for the corresponding evaluation time.

### `placement/`
gives the slice type, x and y slice coordinates for each RO ID.

* `slice_types`
* `x_coordinates`
* `y_coordinates`

## Example dataset sizes
### `ro_frequency_temperature/`

||||
---|---|---
|`axis`||
|	|`board_serialnumbers`|      Dataset \{50}
||	`evaluation_times`    |     Dataset \{1}
||	`repetitions`         |     Dataset \{101}
||	`ro_ids`              |     Dataset \{1600}
||	`temperatures`        |     Dataset \{6}
|`data`||
||	`ro_counts`|                Dataset \{1, 50, 6, 1600, 101}
|`placement`||
||	`slice_types`              |Dataset \{1625}
||	`x_coordinates`            |Dataset \{1625}
||	`y_coordinates`            |Dataset \{1625}

### `ro_frequency_evaluation_time/`
||||
---|---|---
|`axis`||
||	`board_serialnumbers`      |Dataset \{217}
||	`evaluation_times`         |Dataset \{15}
||	`repetitions`              |Dataset \{100}
||	`ro_ids`                   |Dataset \{1600}
||	`temperatures`             |Dataset \{1}
|`data`||
||	`ro_counts`                |Dataset \{15, 217, 1, 1600, 100, 1}
|`placement`||
||	`slice_types`              |Dataset \{1600}
||	`x_coordinates`            |Dataset \{1600}
||	`y_coordinates`            |Dataset \{1600}

