ISSUES WHILE DEPLOYING amazon-kinesis-video-streams-producer-sdk-cpp1.4.1 TO JETSON TX2 SYSTEM



Installing issues:
____________________________________________________________

#1

'__NR_eventfd' undeclared


remedy: 

in install-script to command ./config add no-afalgeng flag: 

>./config  no-afalgeng --prefix=$DOWNLOADS/local/ --openssldir=$DOWNLOADS/local/


#2

checking build system type... ./config.guess: unable to guess system type


remedy:

in install-script after command 
    

>cd $DOWNLOADS/m4-1.4.10	

add

>wget -O config.guess 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.guess;hb=HEAD'
>wget -O config.sub 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.sub;hb=HEAD'

in order to overwrite the obsolete scripts


#3

curl: (77) error setting certificate verify locations:
  CAfile: /etc/ssl/cert.pem

remedy:

sudo mkdir -p /etc/ssl
sudo cp /etc/ssl/certs/ca-certificates.crt /etc/ssl/cert.pem



Running application issues:
____________________________________________________________


#4

error while loading shared libraries: liblog4cplus-1.2.so.5: cannot open shared object file: No such file or directory
 
remedy:

>export LD_LIBRARY_PATH=/home/ubuntu/amazon-kinesis-video-streams-producer-sdk-cpp-1.4.1/kinesis-video-native-build/downloads/local/lib:$LD_LIBRARY_PATH:/usr/lib/aarch64-linux-gnu/tegra/:/usr/lib/aarch64-linux-gnu/gstreamer-1.0
//>export LD_LIBRARY_PATH=/home/ubuntu/amazon-kinesis-video-streams-producer-sdk-cpp-1.4.1/kinesis-video-native-build/downloads/local/lib:$LD_LIBRARY_PATH
//export LD_LIBRARY_PATH=/usr/lib/aarch64-linux-gnu/tegra/:/usr/lib/aarch64-linux-gnu/gstreamer-1.0



#5

gst_element_factory_make ("nvcamerasrc", NULL); returns NULL 

remedy:

>export GST_PLUGIN_PATH=/usr/lib/aarch64-linux-gnu/tegra/:/home/ubuntu/amazon-kinesis-video-streams-producer-sdk-cpp-1.4.1/kinesis-video-native-build/downloads/local/lib/gstreamer-1.0:/usr/lib/aarch64-linux-gnu/gstreamer-1.0:$GST_PLUGIN_PATH
//>export GST_PLUGIN_PATH=/usr/lib/aarch64-linux-gnu/tegra/:/usr/lib/aarch64-linux-gnu/gstreamer-1.0 
//>export GST_PLUGIN_PATH=$LD_LIBRARY_PATH:/usr/lib/aarch64-linux-gnu/tegra/



