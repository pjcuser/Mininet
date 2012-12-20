The following instruction will guide you through how to setup the environment for the [[programming assignment|Assignments]] on Ubuntu. We also provide an Amazon EC2 AMI image with everything set up for people would like to run the lab on EC2 (ami-96139ba6 at Oregon Region). You can find instruction on how to use EC2 AMI image below. 

## Use Your Own Ubuntu Machine
### Install Needed Tools
```no-highlight
sudo apt-get update
sudo apt-get install -y git vim-nox python-setuptools flex bison traceroute
```
### Install Mininet
```no-highlight
cd ~
git clone git://github.com/mininet/mininet
cd mininet
git checkout remotes/origin/class/cs244
./util/install.sh -fnv
```
### Install POX
```no-highlight
cd ~
git clone http://github.com/noxrepo/pox
```

### Install ltprotocol 
```no-highlight
cd ~
git clone git://github.com/dound/ltprotocol.git
cd ltprotocol 
sudo python setup.py install
```

## Use Amazon EC2

The assignments only require t1.micro, which Amazon provides 750 free usage hours per month.  

### Launch an Instance with the provided AMI Image
* Go to [AWS Console](https://console.aws.amazon.com)
* Switch to "Oregon" region, you can do so by pull down the region menu on the upper-right corner. The default is N. Virginia. 
* Click on "Launch an instance", then choose "Classic Wizard"
* On the "Community AMIs", search for "ami-96139ba6". You should see an image with the Manifest of "Mininet_assignments". 
* Select the image, then keep clicking "Continue" on the next few page, until the page ask you to select your key pairs. 
* Choose the key pair you would like to login to your EC2 instance, then click on "Continue". 
* At the final page, you can find an "Launch" button. Click it and you are done!
* Then use your key pair to login to your EC2 instance.
```no-highlight
> ssh -Y -i <Your KeyPair> ubuntu@<your EC2 domain name>
```

The Image contains the starter code for all the assignments. 