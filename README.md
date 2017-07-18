# required hardware 
* [OV528 camera module](https://developer.mbed.org/components/Camera-OV528/)
* mbed board with an SD card slot (I used [NXP K64F](https://developer.mbed.org/platforms/FRDM-K64F/)) or an [SD card shield](https://developer.mbed.org/components/cat/storage/) for boards without an onboard SD card slot
* micro SD card 

# mbed-timelapse

This application takes a photo every 10 minutes and stores the images on an SD card. The application will also save a text file log to the SD card. The application utilized the [mbed OS filesystem](https://docs.mbed.com/docs/mbed-os-api-reference/en/latest/APIs/storage/filesystem/) to store the photos and log.
