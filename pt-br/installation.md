---
layout: default
language: 'pt-br'
version: '4.0'
title: 'Instalação'
keywords: 'instalação, instalando o Phalcon'
---

# Instalação

* * *

![](/assets/images/document-status-stable-success.svg) ![](/assets/images/version-{{ page.version }}.svg)

## Requisitos

### PHP 7.2

Phalcon v4 suporta apenas PHP 7.2 e superior. PHP 7.1 has been released 2 years ago and its [active support](https://www.php.net/supported-versions.php) has lapsed, so we decided to follow actively supported PHP versions. Installing a web server is outside the scope of this document. Please refer to relevant guides on the Internet on how to install a web server.

### PSR

Phalcon requer a extensão PSR. A extensão pode ser baixada e compilada a partir [deste](https://github.com/jbboehr/php-psr) repositório do GitHub. As instruções de instalação estão disponíveis no arquivo `README` do repositório. Depending on the installation method you chose, you might need to add a directive in your `php.ini` so that the PSR extension is loaded.

```ini
extension=psr.so
```

> **NOTE**: You will need the PSR 1.0 extension installed.
{: .alert .alert-danger }

### PDO

Since Phalcon is loosely coupled, it exposes functionality without the need for additional extensions. However, certain components rely on additional extensions to work. When in need for database connectivity and access, you will need to install the `php_pdo` extension. If your RDBMS is MySQL/MariaDB or Aurora, you will need the `php_mysqlnd` extension also. Similarly, using a PostgreSql database with Phalcon requires the `php_pgsql` extension.

### Load order

Phalcon needs to be loaded after `PDO` and `PSR`. Some distributions add a number prefix on `ini` files. If that is the case, choose a high number for Phalcon (e.g. `50-phalcon.ini`), higher than `PDO` and `PSR`. This will load it after the two prerequisite extensions. If however, your distribution only has a `php.ini` file, please make sure that the order is similar to this:

```ini
extension=psr.so
extension=phalcon.so
```

### Hardware

Phalcon is designed to use as little resources as possible, while offering high performance. Although we have tested Phalcon in various low end environments, (such as 0.25GB RAM, 0.5 CPU), the hardware that you will choose will depend on the your application needs.

We have hosted our website and blog for the last few years on an Amazon VM with 512MB RAM and 1 vCPU.

### Software

> **NOTE**: You should always try and use the latest version of Phalcon and PHP as both address bugs, security enhancements as well as performance.
{: .alert .alert-danger }

Along with PHP 7.2 or greater, depending on your application needs and the Phalcon components you need, you might need to install the following extensions:

* [curl](https://www.php.net/manual/en/book.curl.php)
* [fileinfo](https://www.php.net/manual/en/book.fileinfo.php)
* [gettext](https://www.php.net/manual/en/book.gettext.php)
* [gd2](https://www.php.net/manual/en/book.image.php) (to use the [Phalcon\Image\Adapter\Gd](api/Phalcon_Image_Adapter_Gd) class)
* [imagick](https://www.php.net/manual/en/book.imagick.php) (to use the [Phalcon\Image\Adapter\Imagick](api/Phalcon_Image_Adapter_Imagick) class)
* [json](https://www.php.net/manual/en/book.json.php)
* `libpcre3-dev` (Debian/Ubuntu), `pcre-devel` (CentOS), `pcre` (macOS)
* [PDO](https://php.net/manual/en/book.pdo.php) bem como as extensões relevantes do SGDB específico (ex. [MySQL](https://php.net/manual/en/ref.pdo-mysql.php), [PostgreSQL](https://php.net/manual/en/ref.pdo-pgsql.php) etc.)
* [OpenSSL](https://php.net/manual/en/book.openssl.php)
* [Mbstring](https://php.net/manual/en/book.mbstring.php)
* [Memcached](https://php.net/manual/en/book.memcached.php) ou outro adaptador de cache relevante, dependendo do seu uso de cache

> **NOTE**: Installing these packages will vary based on your operating system as well as the package manager you use (if any). Please consult the relevant documentation on how to install these extensions.
{: .alert .alert-info }

For the `libpcre3-dev` package you can use the following commands:

### Pecl

The Pecl installation method is available for Windows, Linux and MacOS. Under windows pre-compiled dll files will be used. Under Linux and MacOS it will compile Phalcon locally so it could be faster to use a different installation method on these platforms. To install using Pecl make sure you have [pecl/pear](https://pear.php.net/manual/en/installation.getting.php) installed.

    pecl channel-update pecl.php.net
    pecl install phalcon
    

#### Debian

```bash
sudo apt-get install libpcre3-dev
```

and then try and install Phalcon again

#### CentOS

```bash
sudo yum install pcre-devel
```

#### Mac/Osx usando Brew

```bash
brew install pcre
```

Without `brew`, you need to go to the [PCRE](https://www.pcre.org/) website and download the latest pcre:

```bash
tar -xzvf pcre-8.42.tar.gz
cd pcre-8.42
./configure --prefix=/usr/local/pcre-8.42
make
make install
ln -s /usr/local/pcre-8.42 /usr/sbin/pcre
ln -s /usr/local/pcre-8.42/include/pcre.h /usr/include/pcre.h
```

For Maverick

```bash
brew install pcre
```

if it gives you error, you can use

```bash
sudo ln -s /opt/local/include/pcre.h /usr/include/
sudo pecl install apc 
```

## Plataformas de Instalação

Since Phalcon is compiled as a PHP extension, its installation is somewhat different than any other traditional PHP framework. Phalcon needs to be installed and loaded as a module on your web server.

### Linux

To install Phalcon on Linux, you will need to add our repository in your distribution and then install it.

#### Distribuições Baseadas em DEB (Debian, Ubuntu, Etc.)

##### Instalação do repositório

Add the repository to your distribution:

**Stable releases**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | sudo bash
```

**Nightly releases**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/nightly/script.deb.sh | sudo bash
```

**Mainline releases (alpha, beta etc.)**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/mainline/script.deb.sh | sudo bash
```

> **NOTA**: Isto só precisa ser feito uma vez, a menos que sua distribuição mude ou você queira mudar de builds estáveis para versões noturnas.
{: .alert .alert-warning }

##### Instalação do Phalcon

To install Phalcon you need to type the following commands in your terminal:

```bash
sudo apt-get update
sudo apt-get install php7.2-phalcon
```

##### PPAs Adicionais

**Ondřej Surý**

If you do not wish to use our repository at [packagecloud.io](https://packagecloud.io/phalcon), you can always use the one offered by [Ondřej Surý](https://launchpad.net/~ondrej/+archive/ubuntu/php/).

Installation of the repo:

```php
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

e do Phalcon:

```php
sudo apt-get install php-phalcon4
```

#### Distribuições baseadas em RPM (CentOS, Fedora, etc.)

##### Instalação do repositório

Add the repository to your distribution:

**Stable releases**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.rpm.sh | sudo bash
```

**Nightly releases**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/nightly/script.rpm.sh | sudo bash
```

**Mainline releases (alpha, beta etc.)**

```bash
curl -s https://packagecloud.io/install/repositories/phalcon/mainline/script.rpm.sh | sudo bash
```

> **NOTA**: Isto só precisa ser feito uma vez, a menos que sua distribuição mude ou você queira mudar de builds estáveis para versões noturnas.
{: .alert .alert-warning }


##### Instalação do Phalcon

To install Phalcon you need to issue the following commands in your terminal:

```bash
sudo yum update
sudo yum install php72u-phalcon
```

##### RPMs Adicionais

**Remi**

[Remi Collet](https://github.com/remicollet) maintains an excellent repository for RPM based installations. You can find instructions on how to enable it for your distribution [here](https://blog.remirepo.net/pages/Config-en).

Installing Phalcon after that is as easy as:

```bash
yum install php72-php-phalcon4
```

Additional versions are available both architecture specific (x86/x64) as well as PHP version specific

#### FreeBSD

Binary package (pkg) and compile myself from source (ports) are available for FreeBSD. To install it you will need to issue the following commands:

##### pkg

```bash
pkg install php74-phalcon4
```

##### ports

```bash
cd /usr/ports/www/phalcon4

make install clean
```

##### Gentoo

An overlay for installing Phalcon can be found [here](https://github.com/smoke/phalcon-gentoo-overlay)

#### Raspberry Pi

```bash
sudo -s
git clone https://github.com/phalcon/cphalcon
cd cphalcon/
git checkout tags/v4.0.0 ./
zephir fullclean
zephir build
```

It is also necessary to increase the swap file from the default 100 MB to at least 2000 MB. Because, the compiler lacks RAM.

```bash
sudo -s
nano /etc/dphys-swapfile
```

Replacing `CONF_SWAPSIZE=100` with `CONF_SWAPSIZE=2000`

After saving the setting, restart the daemon:

```bash
/etc/init.d/dphys-swapfile stop
/etc/init.d/dphys-swapfile start
```

### macOS

Brew includes binary packages so you don't need to compile Phalcon yourself. If you want to compile the extension yourself you need the following dependencies installed:

#### Requisitos de compilação

* Recursos de desenvolvimento PHP 7.x
* XCode

#### Brew

Binary installation (preferred):

```bash
brew tap phalcon/extension https://github.com/phalcon/homebrew-tap
brew install phalcon
```

Compile phalcon:

```bash
brew tap phalcon/extension https://github.com/phalcon/homebrew-tap
brew install phalcon --build-from-source 
```

#### MacPorts

```bash
sudo port install php72-phalcon
sudo port install php73-phalcon
```

Edit your php.ini file and then append at the end:

```ini
extension=php_phalcon.so
```

Restart your webserver.

### PHPBrew (macOS/Linux)

PHPBrew is an excellent way to manage multiple versions of PHP and PHP extensions on your system(s). Installation instructions for PHPBrew can be found [here](https://github.com/phpbrew/phpbrew/wiki/Quick-Start)

If you're using PHPBrew, you can install Phalcon using the following:

```bash
sudo phpbrew ext install phalcon
```

You can install the PSR dependency via phpbrew as well if needed:

```bash
sudo phpbrew ext install psr
```

### Windows

To use Phalcon on Windows, you will need to install the phalcon.dll. We have compiled several DLLs depending on the target platform. The DLLs can be found in our [download](https://phalcon.io/en/download/windows) page.

Identify your PHP installation as well as architecture. If you download the wrong DLL, Phalcon will not work. `phpinfo()` contains this information. In the example below, we will need the NTS version of the DLL:

![phpinfo](/assets/images/content/phpinfo-api.png)

The available DLLs are:

| Arquitetura | Versão | Tipo                  |
|:-----------:|:------:| --------------------- |
|     x64     |  7.x   | Thread safe           |
|     x64     |  7.x   | Non Thread safe (NTS) |
|     x86     |  7.x   | Thread safe           |
|     x86     |  7.x   | Non Thread safe (NTS) |

Edit your php.ini file and then append at the end:

```ini
extension=php_phalcon.dll
```

Restart your webserver.

### Compile From Sources

Compiling from source is similar to most environments (Linux/macOS).

#### Requisitos

* Recursos de desenvolvimento PHP 7.2.x/7.3.x
* Compilador GCC (Linux/Solaris/FreeBSD) ou Xcode (macOS)
* re2c >= 0.13
* libpcre-dev

#### Compilação

Baixe o `zephir.phar` mais recente [daqui](https://github.com/phalcon/zephir/releases). Adicione-o a uma pasta que pode ser acessada pelo seu sistema.

Clone o repositório

```bash
git clone https://github.com/phalcon/cphalcon
```

Compilar o Phalcon

```bash
cd cphalcon/
git checkout tags/v4.0.0 ./
zephir fullclean
zephir build
```

Verifique o módulo

```bash
php -m | grep phalcon
```

You will now need to add `extension=phalcon.so` to your PHP ini and restart your web server, so as to load the extension.

```ini
; Suse: adicionar um arquivo chamado phalcon.ini em /etc/php7/conf.d/ com o seguinte conteúdo:
extension=phalcon.so

; CentOS/RedHat/Fedora: adicionar um arquivo chamado phalcon.ini em /etc/php.d/ com o seguinte conteúdo:
extension=phalcon.so

; Ubuntu/Debian com Apache2: aicionar um arquivo chamado 30-phalcon.ini em /etc/php7/apache2/conf.d/ com o seguinte conteúdo:
extension=phalcon.so

; Ubuntu/Debian com php7-fpm: adicionar um arquivo chamado 30-phalcon.ini em /etc/php7/fpm/conf.d/ com o seguinte conteúdo:
extension=phalcon.so

; Ubuntu/Debian with php7-cli: adicionar um arquivo chamado 30-phalcon.ini em /etc/php7/cli/conf.d/ com o seguinte conteúdo:
extension=phalcon.so
```

The instructions above will compile **and** install the module on your system. You can also compile the extension and then add it manually in your `ini` file:

```bash
cd cphalcon/
git checkout tags/v4.0.0 ./
zephir fullclean
zephir compile
cd ext
phpize
./configure
make && make install
```

If you use the above method you will need to add the `extension=phalcon.so` in your `php.ini` both for CLI and web server.

#### Tuning da Compilação

By default we compile to be as compatible as possible with all processors (`gcc -mtune=native -O2 -fomit-frame-pointer`). If you would like instruct the compiler to generate optimized machine code that matches the processor where it is currently running on you can set your own compile flags by exporting CFLAGS before the build. For example

    export CFLAGS="-march=native -O2 -fomit-frame-pointer"
    zephir build
    

This will generate the best possible code for that chipset but will likely break the compiled object on older chipsets.

### Shared Hosting

Running your application on shared hosting might restrict you in installing Phalcon, especially if you do not have root access. Some web hosting control panels luckily have Phalcon support.

#### cPanel & WHM

cPanel & WHM support Phalcon using Easy Apache 4 (EA4). You can install Phalcon by enabling the [module](https://github.com/CpanelInc/scl-phalcon) in Easy Apache 4 (EA4).

#### Plesk

The plesk control panel doesn't have Phalcon support but you can find installation instructions on the Plesk [website](https://support.plesk.com/hc/en-us/articles/115002186489-How-to-install-Phalcon-framework-for-a-PHP-supplied-by-Plesk-)