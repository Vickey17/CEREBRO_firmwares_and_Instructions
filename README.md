# CEREBRO_firmwares_and_Instructions
Author: Dr. Vikram Pal Singh| Date: 20 Aug 2024

**1.	Firmware setup:**

a.	For flashing the firmware on to the boards, you can use any flashing software, but it is better to use STM32 ST-LINK utility.  Here is the link to download it: https://www.st.com/en/development-tools/stsw-link004.html

b.	Once you have this downloaded, connect the board to the ST-LinkV3 programmer and debugger using the TC2030-CTX-NL-STDC14 tag connect cables. 

c.	Do not forget to power the board using either the GPIO connections (via battery) or using USB-C port and supplying power from a safe 5V port on a laptop or charger brick.

d.	Once the board is powered and connected to the ST-LinkV3, go to> open file and select the correct hex file to flash on the board.

e.	Once correct file is selected, go to Target>> Program and verify. This should flash the firmware on the connected board.

**2.	Firmware:**

a.	There are 3 firmware that can be flashed on the CEREBRO boards:

b.	World_cam_firmware: records a 1200x800 window on the image sensor and then bins it to 600x400 before saving it to SD card. FPS= 63

c.	Eye_cam_firmware: records a 400x400 window. FPS=91

d.	Preview_cam_firmware: allows the user to preview camera frames on a computer screen. This is used during initial fitting to ensure the cameras are placed at correct region of interest.

**3.	Decoding and preview scripts:**

a.	Use the scripts provided in recording_decoding folder to decode the binary files on SD card to get video, frame timestamp for each video and IMU data with timestamps.

b.	For decoding videos, run the 01_run.bat file. It needs 2 arguments i.e. source destination and target destination. 

c.	Open a command terminal and point it to the “recorder_decoder” directory with 01_run.bat file 

for e.g. cd C:\Users\Vikram\Documents\Cerebro_2023\Softwares_and_Firmwares\records_decoder_V1_3_05_24_24\records_decoder

d.	Then run the following command 01_run.bat <source destination> <target destination>

for e.g. 01_run.bat F:\ C:\Users\Vikram\Documents\Cerebro_2023\Data

This will decode the files in the source destination (F:\) and save the decoded data to target destination (C:\Users\Vikram\Documents\Cerebro_2023\Data). If you do not want to copy the raw files, you can use a -b flag while will only decode the data and not copy the raw files.

e.g. 01_run.bat -b <source destination> <target destination>

e.	Note: You need to specify the location for the python binary in the file env.config

f.	Note: For the 1ST run, the system will create a new environment in the folder where 01_run.bat file exists. Be patient as this can take a while. Following this, all the 
other runs should be faster. Overall decoding is a slow process. At the end of the decoding, the command prompt will show length of the videos and statistics of dropped frames.

g.	For previewing the camera view on a computer screen, ensure that preview script is flashed on the board. Connect the board to a computer with USB-C. Open a command 
terminal. Change directory to “recorder-decoder”. Run the 02_run_stream_listener.bat script. 

h.	Once this is running, press the on-board switch and cycle to the preview mode. 
