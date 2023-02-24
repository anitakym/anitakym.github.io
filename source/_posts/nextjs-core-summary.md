---
title: nextjs-core-summary
date: 2023-02-24 15:05:10
tags:
---












### vercel 
```
vercel.json
{
  "version": 2,
  "builds": [
    {
      "src": "./index.js",
      "use": "@vercel/node@2.5.10"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "/"
    }
  ]
}

```