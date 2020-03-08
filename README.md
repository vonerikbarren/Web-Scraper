# Web-Scraper

## Overview
- A web scraper is a tool used to gather information on the internet. Building one uses async code to read sync code and then it can be stored / rendered.

## Pseudocode
1. First create initialize a git repository with README.md
2. clone it to computer
3. move to directory via bash
4. bash: touch webScraper.js
5. bash: npm i puppeteer
6. code: use starter code:

``` javascript
const puppeteer = require('puppeteer');
const browser = await puppeteer.launch({
  headless: false,
});
const page = await browser.newPage();
await page.setRequestInterception(true);
await page.goto('http://www.example.com/');

```

7. bash: launch puppeteer 
8. bash: Use DOM Parser (above code) using document.querySelector.
9. code: if log-in is necessary use type and click methods:

``` javascript
await page.type('#username', 'UsernameGoesHere');
await page.type('#password', 'PasswordGoesHere');
await page.click('button');
await page.waitForNavigation();
```

10. code: to deal with infinite scrolling, use a conditional for loop to gather information:

``` javascript
for (let j = 0; j < 5; j++) {
  await page.evaluate('window.scrollTo(0, document.body.scrollHeight)');
  await page.waitFor(1000);
}

```

11. code: To make code more optimized, you can avoid loading fonts or images for example:
``` javascript
await page.setRequestInterception(true);
page.on('request', (req) => {
 if (req.resourceType() == 'font' || req.resourceType() == 'image'){
   req.abort();
 }
 else {
   req.continue();
 }
}); 
```
