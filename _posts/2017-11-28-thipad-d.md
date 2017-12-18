---
layout: post
title: ubuntu如何调整Thinpad中小红点的速度
---

### 如何设置

首先查看设备ID

```
$ xinput list | grep TrackPoint

↳ TPPS/2 IBM TrackPoint                   	id=13	[slave  pointer  (2)]

```

接下来输出小红帽的相关设置的值

```
$ xinput list-props 13

Device 'TPPS/2 IBM TrackPoint':
	Device Enabled (140):	1
	Coordinate Transformation Matrix (142):	1.000000, 0.000000, 0.000000, 0.000000, 1.000000, 0.000000, 0.000000, 0.000000, 1.000000
	Device Accel Profile (268):	0
	Device Accel Constant Deceleration (269):	0.500000
	Device Accel Adaptive Deceleration (270):	1.000000
	Device Accel Velocity Scaling (271):	10.000000
	Device Product ID (262):	2, 10

```
269是设置其阻力，范围在０～１，本人设置的0.5差不多了，

```
	Device Accel Constant Deceleration (269):	1.000000
	Device Accel Adaptive Deceleration (270):	1.000000
```

最后设置驱动13，　的属性269　的值为0.5

```
xinput set-prop 13 269 0.5
```

完成．