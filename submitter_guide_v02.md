### Submission Guide for sources to contribute to North Star Post's flight tracker

Preface: North Star Post's flight tracking service is in very early stages of development. Your data and comments will assist in improving the process for tracking surveillance flights. This service is provided over the internet, and you should assume that your involvement is being recorded / monitored. For questions on privacy of submission data, please see _Source Confidentiality_ at the end of this document.

This guide assumes that you already have a working instance of dump1090 configured on a Raspberry Pi running Raspbian Wheezy (although Jessie will also work).

To submit data to our tracking service, you will need to install and configure mlat-client to upload data.

mlat-client is still in development and not a part of any Debian / Raspbian archives. It's best to build the latest version from github.

You will need to install the build-essential metapackage and git first to create the package.

`sudo apt-get -y install build-essential git`

Now create a directory to create the package in:  
`mkdir ~/mlat-pkg`

Move to that directory:  
`cd ~/mlat-pkg`

Download the source code using git and cd to the cloned repository:  
`git clone https://github.com/mutability/mlat-client`  
`cd ./mlat-client`

Now create the package  
`dpkg-buildpackage -b -uc`

Install the deb file - *you will need to substitute (version) and (architecture) with the version you downloaded and the architecture for your Raspberry Pi*  
`sudo dpkg -i ../mlat-client_(version)_(architecture).deb`

You may want to run the following command to make sure any missing dependencies are installed:  
`sudo apt-get -f install`

Once you have installed mlat-client, you will need to configure it. You can do so through the post-install setup and/or by modifying /etc/default/mlat-client


##### Here are the key settings:  
Server: polaris.nstarpost.com  
Port: 40147  
Username: If you want alerts, use a valid email address here  
Latitude & Longitude (in decimal form): See steps in *Getting Your Latitude and Longitude*

##### Getting Your Latitude and Longitude
1. Go to http://www.geoplaner.com
2. Type in / locate the address the antenna will be at  
3. Zoom in as close as possible  
4. Click where the antenna is
5. Take note of the decimal latitude & longitude shown in the box titled *dd.ddddd°* , and the elevation (in meters) which is shown in the box titled *elev.* See the screenshot below:  
![Screenshot missing](https://github.com/nstarpost/polaris-user-guide/Lat-Long-Guide.png "Screenshot of geoplaner.com")


## Source Confidentiality  
The North Star Post takes the confidentiality of sources very seriously. We will exercise as much caution as possible in handling any information linkable to you, while using data you submit for our journalistic endeavours.  
Our submission service is currently hosted with Amazon Web Services in their Northern Virginia network. Our service could be surveilled or tampered with at this point, or others along the network without our knowledge.  
We currently accept submissions in unencrypted form over the public internet. This guarantees that your submissions are being monitored by the [US Government](https://en.wikipedia.org/wiki/Upstream_collection) and probably several others. We are investigating possible enhancements to the submission software (mlat-client) that would route this data over the [Tor network](https://www.torproject.org), which may provide improved anonymity.  
If you provide an email address with your submission, this will be shared over the public internet, and with our email providers to deliver messages to you.
