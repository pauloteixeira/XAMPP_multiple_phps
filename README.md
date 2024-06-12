# Configuring XAMPP with multiple PHP Versions
## XAMMP INSTALATION
Download XAMPP 7.2.34 [download](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/7.2.34/xampp-windows-x64-7.2.34-2-VC15-installer.exe/download)

Execute XAMPP Controle Panel as Administratior and click at Config button to change port from :80 to :8080 like the image bellow:
![image](https://github.com/pauloteixeira/XAMPP_multiple_phps/assets/144756/a1132021-e75a-470e-971a-d72f862c1043)

![image](https://github.com/pauloteixeira/XAMPP_multiple_phps/assets/144756/eed42087-4659-47b0-9214-bc067c6542db)

![image](https://github.com/pauloteixeira/XAMPP_multiple_phps/assets/144756/6ac5116d-6f29-471b-a900-1f18124f60b4)



## XAMMP CONFIGURATION
In the https.conf change the DocumentRoot variables like the example bellow

```bash
#DocumentRoot "C:/xampp/htdocs"
#<Directory "C:/xampp/htdocs">
DocumentRoot "C:/Users/paulo.teixeira/Documents/www"
<Directory "C:/Users/paulo.teixeira/Documents/www">
```

Im the httpd-xampp.conf file you will need to add this code in the end of the file

```bash
ScriptAlias /php8/ "C:/xampp/php8/"
<Directory "C:/xampp/php8/">
    AllowOverride None
    Options None
    Require all granted
    <Files "php-cgi.exe">
        AllowOverride None
        Require all granted
    </Files>
</Directory>

Listen 8088
<VirtualHost *:8088>
    UnsetEnv PHPRC
    <FilesMatch "\.php$">
        php_flag engine off
        SetHandler application/x-httpd-php8
        Action application/x-httpd-php8 "/php8/php-cgi.exe"
    </FilesMatch>
</VirtualHost>
```

## SUMARY
That way if you call from Port=8080 will be run the php 7 otherwise if you call from Port=8088 will be run the php 8

![image](https://github.com/pauloteixeira/XAMPP_multiple_phps/assets/144756/faf03434-1a31-4c0c-aece-c4aec1599649)
*PHP 7 Running*

![image](https://github.com/pauloteixeira/XAMPP_multiple_phps/assets/144756/c20e4056-9d6a-40f4-9fc3-b1923385c415)
*PHP 8 Running*

