---
title: Gsoap c++ module in apache server
date: '2017-12-29 15:26:00 +0530'
published: false
---

## Installing a gSoap C++ module in Apache server

The instructions at the [genivia website](https://www.genivia.com/doc/apache/html/index.html) just did not work.

If you are not familiar with how to write a module for Apache, this [blog post](http://theunixtips.com/howto-develop-apache-module-in-c/) will get you started on it. It takes you through the steps of creating a C module and then a C++ module.

The instructions provided by www.genivia.com, ask us to run the following command:  
bin/apxs -a -c -S CC=c++ calcserver.cpp soapC.cpp soapcalcService.cpp stdsoap2.cpp
chmod 755 .lib/calcserver.so

There are no errors whatsoever, so it seems like the command worked and all is well.  
However, when trying to make a soap API call to the installed service, Apache throws the below error:  
gsoap: httpd.conf module mod_gsoap.c SOAPLibrary load "calcserver.so" success, but failed to find the "apache_init_soap_interface" function entry point defined by IMPLEMENT_GSOAP_SERVER()

On closer inspection and by comparison with the "C version" of the gSoap module for the same calulator example, we realized that the DSO (Dynamic Shared Object) created by apxs was different for the "C version" and the "C++ version" of the gSoap module.  

The difference is in the symbols that the DSO exposes. Running nm -C -D calcserer.so on the C and C++ versions show this difference. You may also try this command on the output created in the sample C++ module from the blog post referenced earlier.

There may well be some paramteres to apxs that I am not aware of currently, but it sure is creating some inconsistent behavior. 

To solve the problem, we compiled the "C++ version" of the gSoap module separately as a DSO without using apxs. The command to do that is as follows: