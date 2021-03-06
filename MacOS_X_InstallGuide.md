##Compilation on MacOS

### Qt Installation

Install Qt via: [Qt Download](http://www.qt.io/download/)  

Use default options.  
Add to the PATH environment variable with this temporary solution.  

       export PATH=/users/$USER/Qt/5.5/clang_64/bin:$PATH

Depends on wich version of Qt you use.

###MacPort Installation

Install MacPort and XCode following this guide: [MacPort and XCode](http://guide.macports.org/#installing.xcode)

Start XCode to get it updated and to able C compiler to create executables.  

###Install libraries  

       $sudo port -v selfupdate
       $sudo port install openssl
       $sudo port install miniupnpc
       
For VOIP Plugin: 

       $sudo port install speex-devel
       $sudo port install opencv

Get Your OSX SDK if missing: [MacOSX-SDKs](https://github.com/phracker/MacOSX-SDKs)  

###Last Settings

In QtCreator Option Git add its path:  

       C:\Program Files\Git\bin
       
and select "Pull" with "Rebase"

###Compil missing libraries
####SQLCipher
       
       cd <your development directory>
       git clone https://github.com/sqlcipher/sqlcipher.git
       cd sqlcipher
       ./configure --enable-tempstore=yes CFLAGS="-DSQLITE_HAS_CODEC" LDFLAGS="-lcrypto"
       make 
       sudo make install

NOTE, might be necessary to *chmod 000 /usr/local/ssl* temporarily during *./configure* if 
homebrew uses newer, non-stock ssl dependencies found there. configure might get confused.

####libMicroHTTPD
The one with port don't have good support.

       cd <your development directory>
       wget http://ftpmirror.gnu.org/libmicrohttpd/libmicrohttpd-0.9.46.tar.gz
       tar zxvf libmicrohttpd-0.9.46.tar.gz
       cd libmicrohttpd-0.9.46
       bash ./configure
       sudo make install

You can now compile RS into Qt Creator or with terminal

       cd <your development directory>
       git clone https://github.com/RetroShare/RetroShare.git retroshare
       cd retroshare
       qmake; make

You can find compiled application on *./retroshare/retroshare-gui/src/RetroShare06.app*
