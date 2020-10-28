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

## bashrc/bash_profile tools
```
#enable color for manpages
# Source: https://wiki.archlinux.org/index.php/Man_page#Colored_man_pages
#   mb - begin blinking
#   md - begin bold
#   me - end mode
#   se - end standout-mode
#   so - begin standout-mode (info box)
#   ue - end underline
#   us - begin underline
#
#   LESS_TERMCAP_md=$'\E[01;38;5;74m' \  # nice blue-ish color
#   LESS_TERMCAP_md=$'\E[01;31m' \       # red color

man() {
    env LESS_TERMCAP_mb=$'\E[01;31m' \
    LESS_TERMCAP_md=$'\E[01;31m' \
    LESS_TERMCAP_me=$'\E[0m' \
    LESS_TERMCAP_se=$'\E[0m' \
    LESS_TERMCAP_so=$'\E[01;44;33m' \
    LESS_TERMCAP_ue=$'\E[0m' \
    LESS_TERMCAP_us=$'\E[04;38;5;146m' \
    man "$@"
}

#enable color for perldoc
perldoc() {
    env LESS_TERMCAP_mb=$'\E[01;31m' \
    LESS_TERMCAP_md=$'\E[01;31m' \
    LESS_TERMCAP_me=$'\E[0m' \
    LESS_TERMCAP_se=$'\E[0m' \
    LESS_TERMCAP_so=$'\E[01;44;33m' \
    LESS_TERMCAP_ue=$'\E[0m' \
    LESS_TERMCAP_us=$'\E[04;38;5;146m' \
    perldoc "$@"
}

#convert an IP range into a CIDR(s)
# Usage:
#    iprange2cidr 1.2.3.0 - 1.2.3.255
#           or
#    iprange2cidr "1.2.3.0 - 1.2.3.255"
#
function iprange2cidr() {
    #check for Net::CIDR module
    perl -e "use Net::CIDR" 2>/dev/null
    if [[ $? -eq 2 ]]; then
        echo "[!] ERROR: you do not have the Net::CIDR module installed. Install using sudo cpanm install 'Net::CIDR'"
        return 1
    fi

    #convert the range into a cidr
    perl -M"Net::CIDR ':all'" -e "print join(\"\n\",range2cidr(\"$1$2$3\")).\"\n\""

}

#convert a CIDR into an IP range and give the number of IPs inside the CIDR
function cidr2iprange() {
    #check for Net::CIDR module
    perl -e "use Net::CIDR" 2>/dev/null
    if [[ $? -eq 2 ]]; then
        echo "[!] ERROR: you do not have the Net::CIDR module installed. Install using sudo cpanm install 'Net::CIDR'"
        return 1
    fi

    #check for nmap
    which nmap 2>/dev/null 1>&2
    if [[ $? -eq 1 ]]; then
        echo "[!] ERROR: you do not have nmap installed."
        return 1
    fi

    #convert the cidr to range
    echo -n -e "IP range:\t"
    perl -M"Net::CIDR ':all'" -e "print join(\"\n\",cidr2range(\"$1\")).\"\n\""

    #get the number of ips in the cidr
    echo -n -e "Number of IPs in CIDR:\t"
    nmap -sL $1 | egrep -o "[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}" | sort -u | wc -l
}

#get the AS info for an IP
#  Reference: http://www.team-cymru.org/IP-ASN-mapping.html
ip2asn () {
	whois -h whois.cymru.com " -v $1" ;
}

#grab passwords from passweird.com
#Usage:
#   getpassweird <optional number of passwords to grab>
getpassweird(){

    for i in `seq ${1:-1} `; do
        curl https://www.passweird.com/api/v1/new/ && echo ""
    done

}
```
