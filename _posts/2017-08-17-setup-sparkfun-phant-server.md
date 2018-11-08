---
layout: post
title: setup sparkfun phant server
---
1. github page can not vitualise privately served phant
  Currently I have setup a phant server at a virtual machine maintained by nectar, the installation is quite simple, just do: 
{% highlight bash %}
npm insall -g phant
{% endhighlight %}
  and everything is done. however, github pages provide only https, the self served sparkfun page works only on http. Turns out, a https site can never extract data from http site, which makes github page not able to visualise the data. 
  The first thing i tried was to change the phant server into a https server, this could be achieved by firstly obtain a self signed lisence:
{% highlight bash %}
openssl req -nodes -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 365
{% endhighlight %}
following https://stackoverflow.com/questions/10175812/how-to-create-a-self-signed-certificate-with-openssl
then add the certificate infomation to /usr/local/lib/nodemodules/phant/lib/https/server.js

{% highlight javascript %}
pp.credentials = function() {

  return {
    cert: fs.readFileSync('/opt/certs/example.com.crt'),
    key: fs.readFileSync('/opt/certs/example.com.key')
  };
};
{% endhighlight %}
the problem using this method is that the lisence is not globally accepted but only locally, as a result, once opened up from a webpage, https was crossed out. Turns out the only way of solving this is to obtain a lisence, which would cost a bit.
it seems AJAX works only for https, but this is not true. in fact, github page works only for https, and so it does not allow ajax to retrieve data from http site. the way to get around this issue is actually run the web visualisation site in a http site, not https. So, i have served the webpage in the nectar virtual machine, and problem solved.

2. use 
