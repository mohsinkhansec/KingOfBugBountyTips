## What project KingOfBugBountys?

Our main goal is to share tips from some well-known bughunters. Using recon methodology, we are able to find subdomains, apis, and tokens that are already exploitable, so we can report them. We wish to influence Onelinetips and explain the commands, for the better understanding of new hunters.

[![GitHub followers](https://img.shields.io/github/followers/bminossi.svg?style=social&label=Follow&maxAge=2592000)](https://github.com/bminossi?tab=followers) 
[![GitHub followers](https://img.shields.io/github/followers/OfJAAH.svg?style=social&label=Follow&maxAge=2592000)](https://github.com/OfJAAH?tab=followers)

## Special thanks

- [@Stokfredrik](https://twitter.com/stokfredrik)
- [@Jhaddix](https://twitter.com/Jhaddix)
- [@pdiscoveryio](https://twitter.com/pdiscoveryio)
- [@TomNomNom](https://twitter.com/TomNomNom)
- [@jeff_foley](https://twitter.com/@jeff_foley)


## Scripts that need to be installed

To run the project, you will need to install the following programs:

- [Anew](https://github.com/tomnomnom/anew)
- [Qsreplace](https://github.com/tomnomnom/qsreplace)
- [Subfinder](https://github.com/projectdiscovery/subfinder)
- [Gospider](https://github.com/jaeles-project/gospider)
- [Github-Search](https://github.com/gwen001/github-search)
- [Amass](https://github.com/OWASP/Amass)
- [Hakrawler](https://github.com/hakluke/hakrawler)


###  Search Asn Amass
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/2QnQAyW)

```bash
amass intel -org paypal -max-dns-queries 2500 | awk -F, '{print $1}' ORS=',' | sed 's/,$//' | xargs -P3 -I@ -d ',' amass intel -asn @ -max-dns-queries 2500'
```

###  Using chaos search js
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/32vfRg7)

```bash
chaos -d http://att.com | httpx -silent | xargs -I@ -P20 sh -c 'gospider -a -s "@" -d 2' | grep -Eo "(http|https)://[^/"].*.js+" | sed "s#] - #\n#g" | anew | grep "http://att.com"'
```

###  Search Subdomain using Gospider
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/2QtG9do)

```bash
gospider -d 0 -s "https://site.com" -c 5 -t 100 -d 5 --blacklist jpg,jpeg,gif,css,tif,tiff,png,ttf,woff,woff2,ico,pdf,svg,txt | grep -Eo '(http|https)://[^/"]+' | anew
```

###  Using gospider to chaos
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/2D4vW3W)

```bash
chaos -d http://paypal.com -bbq -filter-wildcard -http-url | xargs -I@ -P5 sh -c 'gospider -a -s "@" -d 3'
```

###  Using recon.dev and gospider crawler subdomains
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/32pPRDa)

```bash
curl "https://recon.dev/api/search?key=apiKEY&domain=paypal.com" |jq -r '.[].rawDomains[]' | sed 's/ //g' | anew |httpx -silent | xargs -I@ gospider -d 0 -s @ -c 5 -t 100 -d 5 --blacklist jpg,jpeg,gif,css,tif,tiff,png,ttf,woff,woff2,ico,pdf,svg,txt | grep -Eo '(http|https)://[^/"]+' | anew'
```

###  PSQL - search subdomain using cert.sh
> @OFJAAAH
> @b51b5b43

- [Explaining command](https://bit.ly/32rMA6e)

```bash
psql -A -F , -f querycrt -h http://crt.sh -p 5432 -U guest certwatch 2>/dev/null | tr ', ' '\n' | grep twitch | anew'
```

###  Search subdomains using github and httpx
> @OFJAAAH
> @b51b5b43

- [Explaining command] - Using python3 to search subdomains, httpx filter hosts by up status-code response (200)

```python
./github-subdomains.py -t APYKEYGITHUB -d domaintosearch | httpx --title
```

###  Search SQLINJECTION using qsreplace search syntax error
> @OFJAAAH
> @b51b5b43

- [Explained comand](https://bit.ly/3hxFWS2)

```bash
grep "="  .txt| qsreplace "' OR '1" | httpx -silent -store-response-dir output -threads 100 | grep -q -rn "syntax\|mysql" output 2>/dev/null && \printf "TARGET \033[0;32mCould Be Exploitable\e[m\n" || printf "TARGET \033[0;31mNot Vulnerable\e[m\n"
```


# Project

[![made-with-Go](https://img.shields.io/badge/Made%20with-Go-1f425f.svg)](http://golang.org)
[![made-with-bash](https://img.shields.io/badge/Made%20with-Bash-1f425f.svg)](https://www.gnu.org/software/bash/)
[![Open Source? Yes!](https://badgen.net/badge/Open%20Source%20%3F/Yes%21/blue?icon=github)](https://github.com/Naereen/badges/)
[![The King](https://aleen42.github.io/badges/src/twitter.svg)](https://twitter.com/ofjaaah)
[![The King](https://aleen42.github.io/badges/src/twitter.svg)](https://twitter.com/b51b5b43)
[![The King](https://aleen42.github.io/badges/src/twitter.svg)](https://twitter.com/willxenoo)
[![Telegram](https://patrolavia.github.io/telegram-badge/chat.png)](https://telegram.com)




<a href="https://www.buymeacoffee.com/OFJAAAH" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 20px !important;width: 50px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>



