# Multiple_websites
Mutiple website hosting at simple steps

-------------------------------------------------- 

# Description

This is a simple multiple website creating scripts using bash script and this is very helphul for your, I belive. 
-------------------------------------------------- 

## Source code
```sh
#! /bin/bash

w_root(){
if [ "$EUID" == 0 ]
then
        w_install
else
        echo "I am exiting from here now"
        exit
fi
}
w_install(){
        echo "Please let me know how many website you would like to host, please choose the below option now"
        echo "1) one website"
        echo "2) Two websites"
        echo "3) Three websites"
read -p "Please choose the value (1|2|3): " Answer
case $Answer in
        1)
                echo "You have selected one website. Please hold a moment whle creating one webiste for you"
                w_onewebsite
        ;;
        2)
                echo "You have selected two websites. Please hold a moment, while creating two website for you"
        ;;
        3)
                echo "You have selected three websites. Please hold a moment, while creating two website for you"
        ;;
        *)
                echo "You have entered invalid option"
        ;;
esac
}
w_onewebsite(){
echo "Installing httpd service"
        yum install httpd -y
        service httpd restart
echo "Please enter the website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainone
mkdir -p /var/www/html/$domainone
cat > /var/www/html/$domainone/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainone.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainone
ServerName $domainone
ServerAlias $domainone
</VirtualHost>
EOF
echo "Restart httpd service and you can check the website on this URL: http://$domainone after adding the hosts file on your local machine"
service httpd restart
echo "The  website is ready and please visit the URL : http://$domainone"
}

w_main(){
        w_root
}
w_main
exit

```
