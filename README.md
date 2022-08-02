This page has the following parts: 
> Robots introduction and assemblies
> Robot configuration and Test run
 > Connecting to the robot
 > Library Setup
 > coding the robot
 
 # Robot Introduction

During your module you will have to be able to use your knowledge to create an autonomous robot with the various inputs that your robot will recieve

## Maratime Robotics - Autonomous boat

** INSERT IMAGE HERE **
Instruction: 

Paste the Word document content here

## Land Rovers
#### Getting Started
You will be allocated 1 of 2 different land robots:

### Pi-Top 
  **INSERT IMAGE HERE**

### Thymio 
  **INSERT IMAGE HERE** 
  
Although they will feature some differences, they will both be run by rasberry pi's and both feature a combination of Odometry, LIDAR and computer vision. 

## Assembly 

A Brief description

## ROS 

Midware such as ROS (Robot Operating System) is included in order for multiple systems to be able to recieve their data from a single wifi source such as the camera system. ROS is used many robotic applications from low to very high budget systems.

Ros will be used in the Land Rover system to read the Lidar sensor data and for for the python code to work with the thymio


## Chrony Setup
Chrony is an implementation of NTP, it allows for the pi's to synchronize their time even if internet is not connected to one of them. It acts as a daemon in the background. So when setup it should never need to be reconfigured or edited with afterwards.
### Synchronizing Chrony Client (Student Pi's)
Go in the Pi terminal
type 'sudo apt-get install vim-y' to install vim, (a unix text editor)
make sure you are connecting to the correct router on the rasberry pi, then to find your ip type 'ip a | grep inet', and copy the third line with 'inet', (may differ: should read something such as '10.10.20.153/24', only copy the fist section, in this case that would be '10.10.20.153'
type 'vim /etc/chrony/chrony.conf'

Below the initial comment, (above all other code) write in a new line: 'server <copied_ip> iburst prefer' where <copied_ip> is the item you have just copied
then finally save the document by pressing Ctrl + C, typing ':x' and pressing Enter. 
(you should have now returned to the original terminal window)
then type 'systemctl restart chrony'
to check if the server is working, type: 'chronyc sources'



# ArUco setup Checklist 

### Before Turning on the Pi 

Ensure Camera is in centre of tank and is facing the tank, (and is connected to the pi) 

Ensure No ArUco Markers Are visible in the Camera frame (flip them upside down to ensure they can’t be seen) 

Ensure that the Router is turned on and that it’s Wifi led is on, (doesn’t need to be connected to the internet) 

Turn On the Rasberry pi, (may take a while, if no monitor attached wait 1 minute to ensure everything has booted up before configuring) 

 

When booting the Pi, the ArUco code should start automatically, therefore it is not necessary to connect a keyboard or mouse to the Pi. If desired, a monitor may be connected to transmit all the Pi’s Information, (recommended). 

 

### When Pi is turned on 

To newly calibrate the origin location, place the Calibration tag (#0) where desired, (ensure it is flat and not moving), the origin will be located in the centre of this marker. Then Show the ‘OK’ (#49) tag in frame. Only when the 2 tags are recognised in frame will the code save the position. 

If you want to use the old Calibrated Origin, then the previous step can be skipped by only showing the ‘OK’ (#49) in frame. 

If the step was done incorrectly, proceed to show the Shut-down tag (#40) together with the ‘OK’ (#49) tag in frame. WAIT 1 minute (to ensure that pi properly switches off), then proceed to turn the pi’s power off then on. (This should reboot the program) 

#### The Setup-phase is now completed 

## Setting Broadcast frequency

The Broadcast Frequency, (frequency at which the Server Pi will send the coordinates to the Client Pi’s) has a possible configuration of ‘logging speed’ (~10th of a second), 1s, 2s, 5s, 10s and never. On boot the pi will be initially setup to send the information every 1s. 

To change the show the desired Broadcast Frequency tag (shown in table below) in frame, with the ‘OK’ tag (#49). 

 

Set Logging speed=#30 

1s=#31, 2s=#32, 5s=#33, 10s=#34, Never=#35  
(remember, these can be changed on the text file inside the aruco folder) 

If a Display is connected to the Pi, the broadcast frequency will be visible as a frame will blink around the screen at every broadcasted interval, (when an ArUco marker is being shown). 

The Server Pi should Now be all set! 

To Turn Off the Pi show the Shut-down tag (#40) together with the ‘OK’ (#49) tag in frame. WAIT 1 minute (to ensure that pi properly switches off).  

The Pi will Log all the ArUco tag information in a csv file of which’ name will be ‘#.csv’ where # is the ArUco Tag’s ID. All these files will be stored in a folder named after the exact time the Pi was booted up, example: ‘2022_07_25_12_34_18’, where is in this order: (‘Year_Month_Day_Hour_Minute_Second’).  

All information will be saved on the ssd card connected separately. This can be disconnected when the Pi is of to read the information from another computer. (there will be a long usb extension so that it is easily accessible). 

 

Setting up the Client Pi’s, (Robots) 

Make sure all packages have been installed and the Chrony configuration have been made. 

Open the Python file  

Run the file  

 

 

 

 

 ## Debugging 

If robot is not receiving information 

Uncomment the ‘print(broadcast_data) line’: 

If nothing the Robot is still not reading anything when any ArUco tag is shown in the camera frame then, (recognised when frame frown around Tag):  

Remember position data will only be broadcasted from the Server Robot once the setup phase is complete) 

Ensure The Client (Robot) Pi is connected to local Router, (called: ArUco) 

Ensure the Port to the one shown on screen from the Rasberry pi, (if so change variable called port to one shown on Server Pi display) 

Ensure no Other code has been altered other than what has been instructed.  

If nothing is still being received please change rasberry pi. 
