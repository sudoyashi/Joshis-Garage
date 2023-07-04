---
layout: post
title: "Cloud resume, Toyotas, and maxing at 65MPH uphill."
author: "Joshua Domingo"
date:   2099-06-23 12:00:00 -1000
tags: technology, it, cloud
categories: cloud
image: 
---

## I'm all fired up after seeing a bunch of Supras and MR2s

Ngl, I got weak seeing a yellow Mk5 Supra parked next to the cab LOL. 

This past weekend I got to hang out with the MR2 crew on O'ahu. Big thanks to Mike for inviting me out, I'll try bring more stuff for the BBQ. For my first time rolling out in a cruise with the cabby, it was a blast. Out of the parking lot, we were planning to go from Waikele Shopping Center to Kualoa beach park. As we were rolling out, I just happened to be behind two Mk5 Supras and as soon as we got on the freeway on-ramp, they lost me! With my foot flat on the floor trying to climb the freeway incline through the Koolau, we were trying our best just to stay within sight of them. Parking at the beach park, we lined up and I had to say thanks to the Supras for trying to stick together. Talking with the Supra guys Fabian, Jimmy, and Zeke, they were sincere about not losing the Golf during that cruise and didn't mind slowing down. At that point, I knew we were all on the same wavelength.




## 2. HTML

Your resume needs to be written in [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML). Not a Word doc, not a PDF. [Here is an example of what I mean](https://codepen.io/emzarts/pen/OXzmym).

## 3. CSS

Your resume needs to be styled with [CSS](https://www.w3schools.com/css/). No worries if you’re not a designer – neither am I. It doesn’t have to be fancy. But we need to see something other than raw HTML when we open the webpage.

## 4. Static Website
Your HTML resume should be deployed online as an [Azure Storage static website](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website). Services like Netlify and GitHub Pages are great and I would normally recommend them for personal static site deployments, but they make things a little too abstract for our purposes here. Use Azure Storage.

## 5. HTTPS

The Azure Storage website URL should use [HTTPS](https://www.cloudflare.com/learning/ssl/what-is-https/) for security. You will need to use [Azure CDN](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal#map-a-custom-domain-with-https-enabled) to help with this.

## 6. DNS

Point a custom DNS domain name to the Azure CDN endpoint, so your resume can be accessed at something like `my-c00l-resume-website.com`. You can use [Azure DNS](https://docs.microsoft.com/en-us/azure/cdn/cdn-map-content-to-custom-domain) or any other DNS provider for this. A domain name usually costs about ten bucks to register.