# LED-Propeller-POV

## Description

This project is a high-speed persistence-of-vision (POV) display that creates images by spinning LED strips on rotating propeller blades. The propellers should be able to rotate at 3,000 RPM and the LEDs are synchronized with the fan's position using a hall effect sensor to create an image in the air. The ESP32 microcontroller should have the bandwidth needed to live stream video to the display in real time.

## Criteria

- Must display readable text + graphic
- ≥ 64 columns × 32 rows
- Image jitter < 2° arc at speed
- Image changeable without stopping (Data stream over WiFi)
- Full RGB

## Calculations

### Speed of fan

To determine the ideal RPM of the fan we need the length of persistance of vision for the average person.

https://sky-lights.org/2023/07/24/qa-persistence-of-vision/ reports the persistance of vision to last 10 - 20ms for the average person so I used 10 milliseconds to calculate ideal RPM.

$ RPM = ((1000 / 10) * 60) / 2 = 3000 $

$10$ is length of persistance of vision.

$1000 / 10$ is the RPS, rotations per second.

The $/2$ is because the fan has 2 propellers each giving their own signal to the eye per rotation.

Note: This is ideal RPM and most LED Propeller fan designs use lower RPM for safety, although a flicker might be visible in-person.

### Clock rate of LED Strip

The clock rate of the LED strip/refresh rate limits the speed of the fan and the number of columns.

$ Hz = (RPM / 60) * N $

$Hz$ is refresh rate in Hertz.

$RPM$ is speed of fan

$N$ is number of columns.

Using 3000 RPM and 64 [columns](#criteria):

$ 3200 = (3000 / 60) * 64 $
