---
title: "Introduction"
date: 2024-03-19T22:47:31-05:00
draft: false
tags: []
description: ""
videoURL: ""
videoTitle: ""
projectTitle: ""
toc: false
layout: ""
---
 
Hello, world. This is the first blog post on my website. As mentioned on the index (home) page of this site, I write blog posts about topics I am learning across the realms of mathematics, computer science, electrical engineering, and everything in between. Additionally, I write about things I am building. 

When I encounter challenges while learning or building, I follow a process (in no particular order) to overcome these obstacles. This includes searching on Google, utilizing 'Google dork' techniques for advanced searches, exploring online forums and blog posts, checking mainstream social media sites, and prompting LLMs (large language models) for assistance. I want to compile all the information and resources I've sifted through to solve a specific problem via these blog posts. Some of the problems I have encountered are very niche and specific, and not much information, if any at all, has been posted online. I aim to help anybody facing similar challenges by compiling the necessary information into one easily digestible webpage, saving time, money, mental bandwidth, and reducing cortisol levels (stress).

I added LaTeX math blocks on the notes. Mathematics. Technicals.
$$
a + b = c
$$

$$
e^x = \sum_{n=0}^{\infty} \frac{1}{n!}x^n = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots
$$

I also added syntax highlighting on the notes.
{{< highlight python >}}
def parse_integer(data: bytes, start_index: int) -> Tuple[int, int]:
    end_index = start_index + 1
    while data[end_index] != ord("e"):
        end_index += 1
    integer_value = int(data[start_index + 1 : end_index])
    return integer_value, end_index + 1
{{< / highlight >}}