---
title: Cross-Origin Resource Sharing (CORS)
slug: cross-origin-resource-sharing-cors
date: 2024-02-27
author: Phat
tags:
  - web-security
image-path: assets/blog/cross-origin-resource-sharing-cors
---

**Supported by Google Gimini*

## Summary

**CORS (Cross-Origin Resource Sharing)** is a security mechanism implemented by web browsers to restrict interactions between resources from different domains. It aims to prevent malicious scripts from accessing sensitive data on other websites.

Here's a summary of CORS:

- **Purpose:** Controls access to resources on a web page from another domain.
- **Functionality:** Achieved through HTTP headers sent by the server, specifying which origins are allowed to access the resource.
- **Benefits:**
    - Enhances web security by preventing unauthorized access to sensitive data.
    - Enables integration between applications from different domains with proper authorization.
- **Common Use Cases:**
    - Embedding images, stylesheets, scripts, iframes, and videos from different domains.
    - Making API requests from a web application to a server on a different domain.

## Browser prevent CORS

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts. For example, fetch() and XMLHttpRequest follow the same-origin policy. This means that a web application using those APIs can only request resources from the same origin the application was loaded from unless the response from other origins includes the right CORS headers.

→ So, browser will prevent CROS, check browser console to see log.

![This is an image](assets/blog/cross-origin-resource-sharing-cors/Untitled.png)

## Server accept CORS for a simple request

The Cross-Origin Resource Sharing standard works by adding new HTTP headers that let servers describe which origins are permitted to read that information from a web browser.

→ So, Server can tell browser that server accept CORS, then browser do not need to prevent request to another origin.

![This is an image](assets/blog/cross-origin-resource-sharing-cors/Untitled%201.png)

## Here are some references for further learning

- **MDN Web Docs:** [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- **Wikipedia:** [https://en.wikipedia.org/wiki/Cross-origin_resource_sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)
- **PortSwigger Web Security Academy:** [https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack](https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack)
