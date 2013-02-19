<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<!-- <meta http-equiv="refresh" content="60" /> -->
<meta http-equiv="X-UA-Compatible" content="chrome=1">
<meta name="description" content="Enabling teredo on Windows Vista+." />
<meta name="keywords" content="Insert,keywords,here" />
<meta name="author" content="Mika Suomalainen" />
<link rel="canonical" href="http://mkaysi.github.com/articles/guides/teredo.html">
<title>Insert title here</title>
<link rel="stylesheet" type="text/css" href="tyyli.css" />
</head>
<body>
<hr/>
[Sitemap](sitemap/sitemap.html)
<hr/>


<!-- vim : set ft=html -->
# Enabling teredo on Windows Vista and above

Linux users: install miredo and start it and you have IPv6. Optionally set 
server in /etc/miredo/miredo.conf .

```
netsh int ipv6 set teredo client teredo.trex.fi
```

Optional, sets Teredo server. The default one is provided by Microsoft,
this isn't, but this is in Finland where I live.

```
route print
```

Scroll up and see what is number of teredo. It's near top.

```
netsh
interface ipv6
show teredo
add route ::/0 interface=XX
```

Replace XX with number from "route print".

```
exit
```

```
netsh interface teredo set state enterpriseclient
```

Optional IF YOUR COMPUTER ISN'T IN DOMAIN! Enterpriseclient can be 
replaced with server or default.

```
regedit
```

Browse to 
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\Dnscache\Parameters

and create a new DWORD (right click somewhere in the middle of window) and 
name it as "AddrConfigControl". It should have value 0 by default, if it 
doesn't, set the value as 0.

<hr/>

<div id="disqus_thread"></div>
<script type="text/javascript">
/* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
var disqus_developer = 0; 
var disqus_url = 'http://mkaysi.github.com/articles/guides/teredo.html';
var disques_title = 'Teredo on Windows Vista and above';
var disqus_shortname = 'mkaysishomepage'; // required: replace example with your forum shortname
/* * * DON'T EDIT BELOW THIS LINE * * */
            (function() {
                var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = 
true;
                dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
                (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0])
.appendChild(dsq);
            })();
        </script>
        <noscript>
Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Dis
qus.</a>
</noscript>
        
<p><a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus
</span></a></p>
<!-- vim : set ft=html -->
</body>
</html>