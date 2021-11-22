# Multiple_websites
Mutiple website hosting at simple steps

-------------------------------------------------- 

# Description
-------------------------------------------------- 

This is a simple multiple website creating scripts using bash script and this is very helphul for you, I belive. 

## Pre-Requestes (Packages Installation)
-------------------------------------------------- 

```sh
sudo yum -y install git 

```
## How to use this script
-------------------------------------------------- 
```sh 

git clone https://github.com/vyjith/multiple_websites.git

cd multiple_websites/

chmod +x multiple_website.sh
```
## Script running
-------------------------------------------------- 
```sh
bash multiple_website.sh

```

## Source code
```sh
#! /bin/bash

w_root(){
if [ "$EUID" == 0 ];
then
        w_install
else
        echo ""
        echo "Please run this script on root privilege, plese switch the user to root using the sudo su -. Thank you"
        echo "I am exiting from here now"
        echo ""
        exit
fi
}
w_install(){
        echo ""
        echo "Please let me know how many website you would like to host, please choose the below option now"
        echo "1) one website"
        echo "2) More than one websites"
        echo ""
read -p "Please choose the value (1|2): " Answer
case $Answer in
        1)
                echo "You have selected one website. Please hold a moment whle creating one webiste for you"
                w_install_httpd
                w_onewebsite
        ;;
        2)      w_install_httpd
                echo ""
                echo -n "Please let me know how many website you would like to host: "
                read y
                x=1
                while [ "$x" -le "$y" ]
                do
                        w_morethanwebsites
                        x=$(( $x +1 ))
                done
                echo ""
                w-restart
        ;;
        *)
                echo "You have entered invalid option"
        ;;
esac
}

w_install_httpd(){
echo ""
echo "Please hold a moment, while checking the required packages installed or not on the server"
echo ""
status="`systemctl show -p ActiveState httpd | sed 's/ActiveState=//g'`"
if [ "$status" = "active" ];
then
        echo ""
        echo "The required packages has been already installed on the server"
        echo ""
else
echo "Installing httpd service"
        yum install httpd -y
        service httpd restart
echo ""
fi
}

w_onewebsite(){
echo ""
echo "Please enter the website name"
echo ""
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainone
if [ -e /var/www/html/$domainone ];
then
        echo ""
        echo "The mentioned domain is already exist on the server"
        echo ""
        exit 1
else
mkdir -p /var/www/html/$domainone
cat > /var/www/html/$domainone/index.html << EOF
Hello World!
EOF
echo ""
echo "We are preparing for you and thank you for your patience"
echo ""
cat > /etc/httpd/conf.d/$domainone.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainone
ServerName $domainone
ServerAlias $domainone
</VirtualHost>
EOF
echo ""
echo "Restart httpd service and you can check the website on this URL: http://$domainone after adding the hosts file on your local machine"
service httpd restart
echo ""
echo "The  website is ready and please visit the URL : http://$domainone"
echo ""
fi
}

w_morethanwebsites(){
echo ""
echo "Please enter the "$x" website name"
echo ""
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainone
if [ -e /var/www/html/$domainone ]
then
        echo ""
        echo "The mentioned domain is already exist on the server"
        echo ""
        exit 1
else
mkdir -p /var/www/html/$domainone
cat > /var/www/html/$domainone/index.html << EOF
Hello World!
EOF
echo ""
echo "We are preparing for you and thank you for your patience"
echo ""
cat > /etc/httpd/conf.d/$domainone.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainone
ServerName $domainone
ServerAlias $domainone
</VirtualHost>
EOF
echo ""
echo "You can check the website after adding the hosts file on your local machine"
echo ""
echo "The  website is ready and please visit the URL : http://$domainone"
echo ""
fi
}
w-restart(){
echo ""
echo "Restarting the httpd service"
service httpd restart
echo ""
echo "httpd resatrted and now you can visit your websites. Thank you and Enjoy : )"
echo ""
}

w_main(){
        w_root
}
w_main
exit
```
