# SquirrleyOneLiners
A list of one-liners I find useful


## Bookmarklets
Search Ultimate Windows Security by Security Event ID
```
javascript:(function(){%20%20%20%20var%20num%20=%20window.prompt("Security%20Event%20ID",%20"");%20%20%20%20var%20url%20=%20"https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid="%20+%20num;%20%20%20%20window.open(url);%20})();
```

Search Ultimate Windows Security by Sysmon Event ID
```
javascript:(function()%20%7B%0A%20%20var%20num%20%3D%20window.prompt(%22Sysmon%20Event%20ID%22%2C%20%22%22)%3B%0A%20%20if%20(num.toString().length%20%3D%3D%201)%20%7B%0A%20%20%20%20var%20url%20%3D%20%22https%3A%2F%2Fwww.ultimatewindowssecurity.com%2Fsecuritylog%2Fencyclopedia%2Fevent.aspx%3Feventid%3D9000%22%20%2B%20num.toString()%3B%0A%20%20%20%20window.open(url)%3B%0A%20%20%7D%20else%20if%20(num.toString().length%20%3D%3D%202)%20%7B%0A%20%20%20%20var%20url%20%3D%20%22https%3A%2F%2Fwww.ultimatewindowssecurity.com%2Fsecuritylog%2Fencyclopedia%2Fevent.aspx%3Feventid%3D900%22%20%2B%20num.toString()%3B%0A%20%20%20%20window.open(url)%3B%0A%20%20%7D%20else%20if%20(num.toString().length%20%3D%3D%203)%20%7B%0A%20%20%20%20var%20url%20%3D%20%22https%3A%2F%2Fwww.ultimatewindowssecurity.com%2Fsecuritylog%2Fencyclopedia%2Fevent.aspx%3Feventid%3D90%22%20%2B%20num.toString()%3B%0A%20%20%20%20window.open(url)%3B%0A%20%20%7D%20else%20if%20(num.toString().length%20%3E%203)%20%7B%0A%20%20%20%20alert(%22Invalid%20Sysmon%20ID%22)%3B%0A%20%20%7D%0A%7D)();
```
