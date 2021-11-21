# Multiple_websites
Mutiple website hosting at simple steps

-------------------------------------------------- 

# Description
-------------------------------------------------- 

This is a simple multiple website creating scripts using bash script and this is very helphul for you, I belive. 

## Source code
```sh
#! /bin/bash

w_root(){
if [ "$EUID" == 0 ]
then
        w_install
else
        echo "Please run this script on root privilege, plese switch the user to root using the sudo su -. Thank you"
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
                w_twowebsite
        ;;
        3)
                echo "You have selected three websites. Please hold a moment, while creating two website for you"
                w_threewebsite
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
w_twowebsite(){

echo "Installing httpd service"
        yum install httpd -y
        service httpd restart
echo "Please enter the first website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainfirst
mkdir -p /var/www/html/$domainfirst
cat > /var/www/html/$domainfirst/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainfirst.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainfirst
ServerName $domainfirst
ServerAlias $domainfirst
</VirtualHost>
EOF
echo "Please enter the second website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainsecond
mkdir -p /var/www/html/$domainsecond
cat > /var/www/html/$domainsecond/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainsecond.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainsecond
ServerName $domainsecond
ServerAlias $domainsecond
</VirtualHost>
EOF
echo "Restart httpd service and you can check the website on this URL: http://$domainfirst &&  http://$domainsecond after adding the hosts file on your local machine"
service httpd restart
echo "The  website is ready and please visit the URL : http://$domainfirst && http://$domainsecond"
}

w_threewebsite(){
echo "Installing httpd service"
        yum install httpd -y
        service httpd restart
echo "Please enter the first website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainfirst
mkdir -p /var/www/html/$domainfirsts
cat > /var/www/html/$domainfirsts/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainfirsts.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainfirsts
ServerName $domainfirsts
ServerAlias $domainfirsts
</VirtualHost>
EOF
echo "Please enter the second website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainseconds
mkdir -p /var/www/html/$domainseconds
cat > /var/www/html/$domainseconds/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainseconds.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainseconds
ServerName $domainseconds
ServerAlias $domainseconds
</VirtualHost>
EOF
echo "Please enter the third website name"
read -p "NOTE: Use lowercase letter and don't use symbols like($,/,*,&,......):" domainthird
mkdir -p /var/www/html/$domainthird
cat > /var/www/html/$domainthird/index.html << EOF
Hello World!
EOF
echo "Please hold a moment"
cat > /etc/httpd/conf.d/$domainthird.conf << EOF
<VirtualHost *:80>
DocumentRoot /var/www/html/$domainthird
ServerName $domainthird
ServerAlias $domainthird
</VirtualHost>
EOF
echo "Restart httpd service and you can check the website on this URL: http://$domainfirsts &&  http://$domainseconds && http://$domainthird after adding the hosts file on your local machine"
service httpd restart
echo "The  website is ready and please visit the URL : http://$domainfirsts && http://$domainseconds && http://$domainthird"
}

w_main(){
        w_root
}
w_main
exit
```
