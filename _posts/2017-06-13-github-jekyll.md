---
layout: post
title: running jekyll in github
---
1. 2017-06-13 13:00 I have followed all the posts to run the jekyll in a github profile but it does not show the page. turns out, I need to modify the post file first, and perhaps clone and upload once to make sure it is working
2. finding the post is not consistent with the files in _posts_  2017-08-17
  usually this is because compilling was error, the way of avoiding this is to check commits (e.g., https://github.com/blogcm/blogcm.github.io/commits/master ) the mark behind each commits tells if this merge is compilled successfully or not

{% highlight python %}
import os
import sys
import numpy as np
#import constants as const
import datetime
class pandas_scale:
    #def __init__(self,file_path,source='raw',fn_csv='scale_merged.csv',fn_hd5='scale_merged.hd5'):
    # http://stackoverflow.com/questions/9867562/pass-kwargs-argument-to-another-function-with-kwargs
    # this is the best way of sorting variables. file_path and sources are
    # variables used for the current init function, while others will be 
    # consumed by subfunctions
    def __init__(self,file_path='None',source='raw',**kwargs ):

        import pdb
        import csv
        import numpy as np
        import pandas as pd
        #import constants as const
        arg_defaults = {
                    'fn_csv' :'scale_merged.csv',
                    'fn_hd5' :'scale_merged.hd5',
                    'names'  :None,
                    'parse_dates':False,
                    'sep' : '\s+',
                    'header':0,
                    'csv_args':None
                       }
        arg=arg_defaults
        for d in kwargs:
            arg[d]= kwargs.get(d)


{% endhighlight %}
below is bash
{% highlight bash %}
#!/bin/bash
# this scripts wirte the detail about what is going to be sent through email
# for example the new ip address, whether the sensors/programs is working and so on.

sleep 17
#su pi
cd /home/pi/pyduino/python/
python loadcell_twolayer_tas606_TE.py

{% endhighlight %}

