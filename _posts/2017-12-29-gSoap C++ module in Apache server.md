---
title: Gsoap c++ module in apache server
date: {}
published: false
---

## Installing a gSoap C++ module in Apache server

The instructions at the [genivia website](https://www.genivia.com/doc/apache/html/index.html) just did not work.

If you are not familiar with how to write a module for APache, this [blog post](http://theunixtips.com/howto-develop-apache-module-in-c/) will get you started on it. It takes you through the steps of creating a C module and then a C++ module.

The instructions provided by www.genivia.com, ask us to run the following command:  
bin/apxs -a -c -S CC=c++ calcserver.cpp soapC.cpp soapcalcService.cpp stdsoap2.cpp
chmod 755 .lib/calcserver.so

There are no errors whatsoever, so it seems like the command worked and all is well.  
However, when trying to make a soap API call to the installed service, Apache throws the below error:  
gsoap: httpd.conf module mod_gsoap.c SOAPLibrary load "/emc/krishv16/apachegsoap/bar/.libs/calcserver.so" success, but failed to find the "apache_init_soap_interface" function entry point defined by IMPLEMENT_GSOAP_SERVER()