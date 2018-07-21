# WordPress-Password-Reset-Command-Tool
You can reset WordPress Password with Single Command on any cPanel server

1  You will need to install WP command tool on the server. You can install it with below steps

----------------------
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x wp-cli.phar
mv wp-cli.phar /usr/local/bin/wp
----------------------

2 Create wppasswd command 

Create the file  /usr/local/bin/wppasswd  and insert code of file https://github.com/cloudhostworld/WordPress-Password-Reset-Command-Tool/blob/master/Command-code

------------------
cpanel_username=`grep  ${@} /etc/userdomains | awk '{print $2}'`
documentroot=`grep documentroot /var/cpanel/userdata/$cpanel_username/${@} | awk '{print $2}'`
cd $documentroot
wppassword=$(</dev/urandom tr -dc '12345!&*#%qwertQWERTasdfgASDFGzxcvbZXCVB' | head -c13; echo "")
#read -p " Choose WordPress Password :- " wppassword;
wpuser=`wp user list --allow-root | awk {'print $2'} | grep -v user_login`
wp user update $wpuser --user_pass="$wppassword" --allow-root
echo "================================================================="
echo "WordPress Details are as follows"
echo ""
echo "Website Name : ${@}"
echo "Username: $wpuser"
echo "Password: $wppassword"
echo ""
echo "================================================================="
-------------------

chmod +x wp-cli.phar

You can reset password of any WordPress domain . 
For Example  

wppasswd  cloudhostworld.com

