# required hardware
* [OV528 camera module](https://developer.mbed.org/components/Camera-OV528/)
* mbed board with an SD card slot (I used [NXP K64F](https://developer.mbed.org/platforms/FRDM-K64F/)) or an [SD card shield](https://developer.mbed.org/components/cat/storage/) for boards without an onboard SD card slot
* micro SD card

# mbed-timelapse
This application takes a photo every 10 minutes and stores the images on an SD card. The application will also save a text file log to the SD card. The application utilized the [mbed OS filesystem](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/APIs/storage/filesystem/) to store the photos and log.

I let my timelapse run for two weeks. This introduced some interesting requirements:

* **Logging** - When running in the short term, I relied on capturing `STDOUT` from the board with a serial connection to my computer. As the device was going to be running without any PC connection, I needed a way to check that the application was still working as intended. I used a [logging function](https://github.com/sarahmarshy/mbed-timelapse/blob/master/main.cpp#L16) to write any messages to a file, which I could view later on the SD card.
* **Continuous naming scheme** - To make the timelapse, I would need to know the order in which photos were taken. Without a [persistent RTC](https://en.wikipedia.org/wiki/Real-time_clock), I relied on a naming scheme. So, they'd need to be named in order. I chose `img0`, `img1`...`imgN`. However, between power cycles, the device would lose this count. I chose to [make a new directory](https://github.com/sarahmarshy/mbed-timelapse/blob/master/main.cpp#L93-L122) with each power cycle, such that they would be named `dir0`, `dir1`...`dirN`. When the application starts, it finds the first `dirX` that does not exist and creates it. Within each of these directories, images were named according to `img0`, `img1`...`imgN`, using a [global count variable](https://github.com/sarahmarshy/mbed-timelapse/blob/master/main.cpp#L12) to keep track of the image number.
