# Install Latest [pycURL](http://pycurl.io/) from Source On CentOS 7

## Install Dependencies
* Install `python-devel`

       sudo yum install -y python-devel

* [Install Latest cURL from Source on CentOS 7](https://github.com/northbright/Notes/blob/master/curl/install-latest-curl-from-source-on-centos-7.md)
   * It'll install latest [OpenSSL](https://www.openssl.org/) and compile cURL with it
   * Make sure compile [pycURL](http://pycurl.io/)  using the same version of [OpenSSL](https://www.openssl.org/) 

## Download Source from [Offical Git Repo](https://github.com/pycurl/pycurl/releases)

    cd download
    wget https://github.com/pycurl/pycurl/archive/REL_7_43_0_2.tar.gz
    tar -xzvf REL_7_43_0_2.tar.gz
    cd pycurl-REL_7_43_0_2

## Configure and Install
```
// Clean
sudo make clean

// Generate files
make gen

// Run PIP install with --ignore-installed option
sudo PYCURL_CURL_CONFIG=/usr/local/curl/bin/curl-config PYCURL_SSL_LIBRARY=openssl CPPFLAGS="-I/usr/local/openssl/include" LDFLAGS="-L/usr/local/openssl/lib" pip install . --ignore-installed
```

## Add New Shared Libraries Path of cURL
 
    su
    echo '/usr/local/curl/lib/' > /etc/ld.so.conf.d/curl.conf
    exit
    sudo ldconfig
            
    # Check
    ldconfig -p | grep libcurl

## References
* [PycURL Installation](http://pycurl.io/docs/latest/install.html)
* [yum Failed after Install cURL from Source on CentOS 7](https://github.com/northbright/Notes/blob/master/Linux/CentOS/yum/yum-failed-after-install-curl-from-source-on-centos-7.md)
* [编译安装curl后，使用yum报错 pycurl.so: undefined symbol: CRYPTO_num_locks](https://xvcat.com/post/1429)
* [Yum commands error "pycurl.so: undefined symbol: CRYPTO_set_locking_callback"](https://access.redhat.com/solutions/641093)
