# Awesome GINS Dataset

## An awesome GINS dataset for GNSS/INS integration applications

<img src="./GNSS RTK/Map.jpg" style="zoom:50%" />

This repository provide an awesome GINS dataset for GNSS/INS integration applications. The biggest feature of the dataset is that four different grade MEMS IMUs are included, which provide an opportunity for the researches to comprehensively evaluate their algorithms.

The dataset was collected in an open-sky industrial area, where the GNSS RTK was well satisfied. The duration of the whole dataset is 1617 seconds, including the raw IMU data, GNSS RTK positioning results, and the ground-truth for each IMU.

**Authors:** Hailiang Tang, Xiaoji Niu, and Tisheng Zhang from the [Integrated and Intelligent Navigation Group](http://www.i2nav.com/), Wuhan University.

**Related Paper:**

- ...

## 1 The MEMS IMU

Four MEMS IMUs are included in this dataset, and the details about these IMUs are listed as follows:

| IMU         | Description             | Vendor         | Gyroscope Bias Instability (Allan Variance) [$\deg/hr$] |
| ----------- | ----------------------- | -------------- | ------------------------------------------------------- |
| ICM20602    | consumer-grade chip     | InvenSense     | 10.0                                                    |
| ADIS16460   | industrial-grade module | Analog Devices | 8.0                                                     |
| ADIS16465   | industrial-grade module | Analog Devices | 2.0                                                     |
| HGuide-i300 | industrial-grade module | Honeywell      | 3.0                                                     |

We also provide a set of noise parameters for each IMU, which are obtained by conducting parameter tuning. Specifically, the IMU measurements are defined as follows: 
$$
\boldsymbol{\tilde{f}}^{\mathrm{b}}=\boldsymbol{f}^{\mathrm{b}}+\boldsymbol{b}_a+\boldsymbol{n}_a, 
\\
\boldsymbol{\tilde{w}}_{\mathrm{ib}}^{\mathrm{b}}=\boldsymbol{w}_{\mathrm{ib}}^{\mathrm{b}}+\boldsymbol{b}_g+\boldsymbol{n}_g
$$
where the additive noise $\boldsymbol{n}_a$ and $\boldsymbol{n}_g$ are modeled as Gaussian white noise processes; $\boldsymbol{b}_a$ and $\boldsymbol{b}_g$ are respectively the accelerometer and gyroscope biases, which are modeled as first-order Gaussian Markov processes. The IMU noise model can be expressed as follows:
$$
\boldsymbol{n}_g\sim \mathcal{N} \left( \mathbf{0},\sigma _{g}^{2}\boldsymbol{I} \right) , 
\\
\boldsymbol{n}_a\sim \mathcal{N} \left( \mathbf{0},\sigma _{a}^{2}\boldsymbol{I} \right) ,
\\
\delta \boldsymbol{\dot{b}}_{g_t}=-\frac{1}{\tau _{b_g}}\delta \boldsymbol{b}_{g_t}+\boldsymbol{n}_{b_g}, \boldsymbol{n}_{b_g}\sim \mathcal{N} \left( \mathbf{0},\sigma _{b_g}^{2}\boldsymbol{I} \right) ,
\\
\delta \boldsymbol{\dot{b}}_{a_t}=-\frac{1}{\tau _{b_a}}\delta \boldsymbol{b}_{a_t}+\boldsymbol{n}_{b_a}, \boldsymbol{n}_{b_a}\sim \mathcal{N} \left( \mathbf{0},\sigma _{b_a}^{2}\boldsymbol{I} \right)
$$

The reference noise parameters are listed as follows:

| IMU         | Angle Random Walk<br /> $\sigma_g$ [$deg/\sqrt{hr}$] | Velocity Random Walk<br />$\sigma_a$ [$m/s/\sqrt{hr}$] | Gyroscope-bias Standard Deviation<br />$\sigma_{b_g}$ [$deg/hr$] | Accelerometer-bias Standard Deviation<br />$\sigma_{b_a}$ [$mGal$] | Correction Time<br />$\sigma_g, \sigma_a$ [$hr$] |
| ----------- | ---------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------ |
| ICM20602    | 0.2                                                  | 0.2                                                    | 200                                                          | 1000                                                         | 1                                                |
| ADIS16460   | 0.2                                                  | 0.1                                                    | 20                                                           | 100                                                          | 1                                                |
| ADIS16465   | 0.1                                                  | 0.1                                                    | 25                                                           | 200                                                          | 1                                                |
| HGuide-i300 | 0.2                                                  | 0.2                                                    | 15                                                           | 150                                                          | 1                                                |

## 2 Installation parameters

The IMU body frame (b-frame) is defined as forward-right-down (FRD) coordinate. The GNSS geodetic positioning is defined in WGS-84 ellipsoid model. The GNSS antenna lever-arms in b-frame are listed as follows:

| IMU         | Lever-arms (FRD) [$m$] |
| ----------- | ---------------------- |
| ICM20602    | -0.073, 0.302, 0.087   |
| ADIS16460   | 0.045, 0.46, -0.238    |
| ADIS16465   | -0.073, 0.302, 0.087   |
| HGuide-i300 | -0.075, 0.46, -0.218   |

## 3 File format descriptions

Three type of files are contained in the dataset, including the IMU binary file, the GNSS positioning result text file, and the ground-truth text file.

The IMU binary file format (*.bin) is defined as:

| Field | Type   | Bytes | Description                 | Units |
| ----- | ------ | ----- | --------------------------- | ----- |
| 1     | double | 8     | GNSS seconds of week        | $s$   |
| 2     | double | 8     | incremental angle x axis    | $rad$ |
| 3     | double | 8     | incremental angle y axis    | $rad$ |
| 4     | double | 8     | incremental angle z axis    | $rad$ |
| 5     | double | 8     | incremental velocity x axis | $m/s$ |
| 6     | double | 8     | incremental velocity y axis | $m/s$ |
| 7     | double | 8     | incremental velocity z axis | $m/s$ |

The GNSS positioning result text file (*.pos, 7 columns) is defined as:

| Field | Description                  | Units |
| ----- | ---------------------------- | ----- |
| 1     | GNSS seconds of week         | $s$   |
| 2     | geodetic latitude            | $deg$ |
| 3     | geodetic longitude           | $deg$ |
| 4     | geodetic height              | $m$   |
| 5     | latitude standard deviation  | $m$   |
| 6     | longitude standard deviation | $m$   |
| 7     | height standard deviation    | $m$   |

The ground-truth text file (*.nav) is defined as:

| Field | Description                 | Units |
| ----- | --------------------------- | ----- |
| 1     | GNSS week                   | -     |
| 2     | GNSS seconds of week        | $s$   |
| 3     | geodetic latitude           | $deg$ |
| 4     | geodetic longitude          | $deg$ |
| 5     | geodetic height             | $m$   |
| 6     | velocity in north direction | $m/s$ |
| 7     | velocity in east direction  | $m/s$ |
| 8     | velocity in down direction  | $m/s$ |
| 9     | roll attitude               | $deg$ |
| 10    | pitch attitude              | $deg$ |
| 11    | yaw attitude                | $deg$ |

