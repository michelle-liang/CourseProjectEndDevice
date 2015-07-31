﻿Course Project End Device Part 
========================

Summary:
------------------------

This project is mainly about how to use RESTful web service in the IOT project ,basically It is how to set up a running system with both a device get the real data and a  server store and display the data. I will talk in detail about how to set up the running system first, and then I will talk about how the hardware and software 's functions and how they work together. which works together out-of-the-box.

The System Architecture:
------------------------

              
            1st Level       Web Browser 
     
                              |     |
            2nd Level       RESTful Server
                             |        |
                            |          |
            3rd Level  End Device   End Device


setting up the system 
------------------------
Then I am going to talk about how to make the system work , be sure you have downloaded all the code  !! and import them in the eclipse projects , by the way I am using eclipse for setting up this system not in the raspberry but in my local PC .If you really want to programming in the raspberry pi ,you can do it ,but I am sure it is very slow .you can use my projects also ,cause you still can use maven in the raspberry pi. I am going to lead you guys from both hardware and software side.

 Hardware:
1. the raspberry OS:
	The first is you need to install and configure the system in the raspberry pi ,which using as SD card as its memeory and storage ,I am not going to talk about how to install the r aspberry OS here you can find more tutorials here: https://www.raspberrypi.org
2.The connection of the DHT11 temp sensor and the device 
              2.1 connect temp sensor
              you need three wires to get data from the DHT11 sensor, which is power/ground/data
    below is my connection:
                              
                                                             













               I mainly get the inspiration from this website: http://hirt.se/blog/?p=493









	2.2 connect the relay device
              relay something is just like relay a led device ,you only need to wires to relay a device which is state and ground: connection like below:
             
	   










 


  

3.the xbee connection :
   for the xbee connection you may need using XCTU for confire the xbee :
http://www.libelium.com/development/waspmote/documentation/x-ctu-tutorial/
   for how to configure the xbee different mode learn form here:
 http://www.arduino-hacks.com/xbee-api-mode/
  below is my configure: 
1. for end device:

















2. for server device:
   


















after you plugin the xbee device into your system use command below:
             ls /dev/tty
 you will get a device named 
          “ttyUSB*” * means numbers:

 
    Software:
    After the hardware part is done! You need to install some libraries and configure to make the system runing.
0. install DHT-11 driver :
            download code from here:   https://github.com/adafruit/Adafruit-Raspberry-Pi-Python-Code/tree/master/Adafruit_DHT_Driver 
             cd into this folder and then using the command  : make 
             you will get a runnable file Adafruit_DHT;
             put it into you PATH environment.
 
1. install jdk8
           download  form here http://www.oracle.com/technetwork/java/javase/downloads/jdk8-arm-downloads-2187472.html
              unzip it into somewhere I installed it in /opt/java 
		cd /opt/java/yourjdkversion/
		sudo update-alternatives --install "/usr/bin/java" "java" 							"/opt/java/yourjdkversion/java" 1
		sudo update-alternatives --set java /opt/java/ejre1.7.0_10/bin/java

		open /etc/profile add those lines in the bottom:
			export JAVA_HOME=/opt/ yourjdkversion

			export JRE_HOME=$JAVA_HOME/jre 

			export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib 

			export PATH=$JAVA_HOME/bin:$PATH 
		Now you should be able to execute java

2. install java serial tools
 		You can install RXTX like this:
		$ sudo apt-get install librxtx-java
3.set up the end device part 
     Be sure you have download maven2 .if you haven't run below command in the command line:
          sudo apt-get install maven2
     Be sure you have download 
                 CourseProject : https://github.com/wentixiaogege/CourseProject   ;
		CourseProjectEndDevice: https://github.com/wentixiaogege/CourseProjectEndDevice;
     import those projects into your eclipse you will see all the avaibleable code,make sure there is no error show up.
       
                 












	cd to the CourseProject folder and then run below:
                         mvn clean install 
        cd to the CourseProjectEndDevice folder and then run below :
                         mvn clean install 
        everything shoul went well and then you will get a XXXX.jar package like below:

                    

















      copy and paste this XXXX.jar package into your raspberry OS system anywhere you want and run the below command:
      sudo java -Djava.library.path=/usr/lib/jni/ -jar yourpackagename.jar 

and you are set .!!!!!!!







