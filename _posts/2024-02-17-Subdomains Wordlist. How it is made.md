---
title: Subdomains Wordlist - How it is made?
date: 2024-02-17 22:30:00 +0530
categories: [subdomains_wordlist]
tags: [subdomains_wordlist subgen]     # TAG names should always be lowercase
---

Hi there!

I hope you are doing well

Recently, I create a new github repository, for subdomain wordlist. The repo can be found at [https://github.com/shriyanss/subdomains_wordlist](https://github.com/shriyanss/subdomains_wordlist)

This repository contains multiple wordlists, but they are generated from a same dataset. So first of all, I'll tell you how this dataset is obstained

## How the dataset is obtained?
The tool first of all gets the subdomains for different domains. The list of domains is obtained from [@arkadiyt/bounty-targets-data/data/domains.txt](https://github.com/arkadiyt/bounty-targets-data/blob/main/data/domains.txt) (thanks to [@arkadiyt](https://github.com/arkadiyt) for this repo ;) )

Since this is too raw to undergo further process, I first of all, get all the domains with the help of a custom python script that extracts domains from it. By me telling this is raw, I mean that there are programs that add `app.target.com` in the scope. So from that, I am not interested in `app` or the something else, but I am interested in the domain.

Once I've got the domains, the next step is obviously subdomain enumeration. A bash script does this thing. But before I pass everything to it, I made another python script, that divides `X` number of domains into a file, for which it has to do subdomain enumeration. This is because I don't want my machine to just blast up doing subdomain enumeration for the whole week, which might saturate the system for other processes. The script I am talking about, simply reads a file called `last.txt`, and gives the next `X` number of domains from the domains file. Also, if it reaches end of the file, it starts from the top to complete that `X` *\*criteria\**.

At this point, our dataset to be processed is ready.

> At the time of writing this blog, I had nearly 1 million subdomains. This count can easily increase later

## Generating wordlist
Once it has got the subdomain list, it simply runs my own tools [`subgen`](https://github.com/shriyanss/subdomain_wordlist_gen), and hence, a raw [`wordlist.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/wordlist.txt) is complete. But the thing is that, it's not actually a wordlist. It's just a raw dump of subdomains from different companies.

The next that is to be done is to remove some prominent noise from the wordlist. Currently, I manually scroll though the list, and identify any pattern of noise. For example, the subdomains containing just numbers and `-` are less useful, and are also prominent in the wordlist. So I simply remove them. There are more similar noise patterns that are removed from the wordlist, and then piped into [`no_number.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/no_number.txt), [`no_uuid.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/no_uuid.txt) and others.

The file [`filtered_subdomain_wordlist.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/filtered_subdomain_wordlist.txt) is a combination of the above two (no UUID and numebers) file and multiple other patterns I've identified.

The next comes [`frequent.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/frequent.txt). First of all, generation of this file takes the longest. What it does is it iterates through the [`filtered_subdomain_wordlist.txt`](https://github.com/shriyanss/subdomains_wordlist/blob/main/filtered_subdomain_wordlist.txt), and then check the occurance of current line. Like it first goes to the first line, and it contains `www` (suppose), next it iterates through the whole file, and gets count of it. I know this process is less efficient, but it can be improved later on when it gets really slow. The number of times, is currently set to 5. Meaning, if any subdomain has a frequency of 5 in the `subdomains.txt`, then it will be included in the frequent wordlist. I might change this later, on the basis of noise I get, or maybe seperate them in different files.


I hope this was informative. See you next time :)

Also, feel free to star the wordlist repo. Link: [https://github.com/shriyanss/subdomains_wordlist](https://github.com/shriyanss/subdomains_wordlist)

> Pull requests related to grammar or missing content or anything is always welcome (but not spam) :)
>
> *Update README.md*
