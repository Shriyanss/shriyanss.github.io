---
title: Projects
icon: fas fa-file-code
order: 4
---

# Projects I've made

## [vhost-master](https://github.com/shriyanss/vhost-master)
VHost Master is a virtual host bruteforcing tool. It works as follows:-
- You provide it with a subdomains list for a domain
- It resolves them into IP addresses and then gets the IP addresses which has multiple subdomains
- Then it startesstarts bruteforcing virtual hosts on them


## [subdomain_wordlist_gen](https://github.com/shriyanss/subdomain_wordlist_gen) (aka subgen)
Subgen is a subdomain word list generator utility. You can just provide it a subdomains list you've enumerated from any of the tools, and then based on that, it generates a wordlist

## [subdomains_wordlist](https://github.com/shriyanss/subdomains_wordlist)
This repository is a collection of subdomain wordlists generated with help of [subgen](https://github.com/shriyanss/subdomain_wordlist_gen).

It has a few more scripts running to filter out noise. The wordlist is generated everyday (as of Feb 13th 2024). The generation of the wordlist starts at 00:00 IST and the end time (at which the wordlist is updated in the repo) depends on the size. You can easily expect it to take 12 hrs or more to be updated.