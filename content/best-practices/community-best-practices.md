---
title: "Community Best Practices"
date: 2020-09-05T03:14:55+01:00
draft: 
---

## ProcessMaker Best Practices from the Community

Below is a list of Best Practices from ProcessMaker developers

#### [Ayodeji Idowu](https://www.linkedin.com/in/ayodeji-idowu-26b317115/)

Well in my experience using ProcessMaker I try to do a few things that can make development faster:
1. I have subforms with their corresponding js implements that are reusable e.g Account Number Input and Display, Comment Section Input and Display, Mandate Display, etc. With this, I can easily reduce the amount of time used in designing the forms every time it is needed for a new project. This also helps uniformity when you work out of a large team of designers

2. I also have a javascript file that contains snippets of code. This file is stored in the public_html file and it is referenced from the external libs field of the dynaforms. This reduces the amount of javascript you need to write in any project.

3. For RSA encryption when calling APIs that require such feature you can implement the encrypt.js library and reference it from the external libs field of the dynaforms
