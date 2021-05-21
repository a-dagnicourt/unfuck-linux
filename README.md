# unfuck-linux
How to reinstall Linux &amp; co in less than 2 days after you totally fucked it up.

![alt text](https://github.com/a-dagnicourt/unfuck-linux/blob/main/assets/terminal.png "Much wow")

# [ZSH + Oh My Zsh + Powerlevel10k + tacticool stuff](https://dev.to/abdfnx/oh-my-zsh-powerlevel10k-cool-terminal-1no0)

```zsh
sudo apt install zsh
zsh
chsh
```

```zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
vim ~/.zshrc
```

_ZSH_THEME="powerlevel10k/powerlevel10k"_
_Set terminal font : FiraCode Nerd Font_
_Restart terminal_

```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

### [Ruby (for gems use)](https://gorails.com/setup/ubuntu/20.04)

```zsh
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update
sudo apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn
```

```zsh
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
```

```zsh
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
rbenv install 3.0.1
rbenv global 3.0.1
ruby -v

gem install bundler
```

(I hate Ruby now.)

```zsh
gem install colorls
vim ~/.zshrc
```

_source $(dirname $(gem which colorls))/tab_complete.sh_
_plugins=( git zsh-syntax-highlighting zsh-autosuggestions )_
_if [ -x "$(command -v colorls)" ]; then_
_alias ls="colorls"_
_alias la="colorls -al"_
_fi_

```zsh
source ~/.zshrc
```

# SSH Keys for Git

```zsh
ssh-keygen
cat ~/.ssh/id_rsa.pub
eval $(ssh-agent)
ssh-add ~/.ssh/id_rsa
```

# Nodejs + nvm + npm

```zsh
sudo apt install nodejs
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | zsh
nvm list-remote
nvm install v16.0.0
```

# [LAMP Stack](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04)

### Apache2

```zsh
sudo apt install apache2
sudo ufw allow in "Apache"
sudo ufw status
```

-> if inactive :

```zsh
sudo ufw enable
sudo ufw status
sudo service apache2 start
```

### Mysql

```zsh
sudo apt install mysql-server
sudo service mysql start
sudo mysql_secure_installation
```

### [PHP](https://www.tecmint.com/install-php-8-on-ubuntu/)

```zsh
sudo apt update && sudo apt upgrade
sudo apt install ca-certificates apt-transport-https software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.0 libapache2-mod-php8.0
sudo service apache2 restart
sudo apt install php8.0-bz2 php8.0-calendar php8.0-ctype php8.0-curl php8.0-date php8.0-exif php8.0-fileinfo php8.0-filter php8.0-ftp php8.0-gd php8.0-gettext php8.0-gmp php8.0-hash php8.0-iconv php8.0-intl php8.0-json php8.0-libxml php8.0-mbstring php8.0-openssl php8.0-pcntl php8.0-pcre php8.0-posix php8.0-readline php8.0-Reflection php8.0-session php8.0-shmop php8.0-sockets php8.0-sodiumphp8.0-ssh2 php8.0-standard php8.0-sysvmsg php8.0-sysvsem php8.0-sysvshm php8.0-tokenizer php8.0-uuid php8.0-xdebug php8.0-opcache php8.0-zlib
touch /var/www/html/info.php && vim /var/www/html/info.php
```

### [PHPMyAdmin](https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04-fr)

```zsh
sudo apt update
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

sudo mysql
```

```sql
mysql> UNINSTALL COMPONENT "file://component_validate_password";
mysql> exit
```

```zsh
sudo apt install phpmyadmin

sudo mysql
```

```sql
mysql> INSTALL COMPONENT "file://component_validate_password";
```

```zsh
sudo phpenmod mbstring
sudo service apache2 restart

sudo mysql
```

```sql
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
```

```zsh
sudo service apache2 restart

sudo vim /etc/apache2/conf-available/phpmyadmin.conf
```

_AllowOverride All under DirectoryIndex index.php_

```zsh
sudo service apache2 restart

sudo vim /usr/share/phpmyadmin/.htaccess
```

_AuthType Basic_
_AuthName "Restricted Files"_
_AuthUserFile /etc/phpmyadmin/.htpasswd_
_Require valid-user_

```zsh
sudo htpasswd -c /etc/phpmyadmin/.htpasswd username
```

### [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos)

```zsh
cd

sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php composer-setup.php
sudo php -r "unlink('composer-setup.php');"
```

Global install :

```zsh
sudo mv composer.phar /usr/local/bin/composer
```

(Nice tech bro.)
