---
{"dg-publish":true,"permalink":"/playwright-intro-ts-tau/chapter-5-1-troubleshooting-test-issues/","created":"","updated":""}
---

links:: [[playwright-intro-ts-tau/introduction to playwright typescript MOC\|introduction to playwright typescript MOC]]

# Chapter 5.1 - Troubleshooting Test Issues

## Chapter 5.1 - Troubleshooting Test Issues

1. Turn on trace and screenshots in config file for failures (see below)


```playwright.config.ts

    trace: 'retain-on-failure',
    // trace: 'on-first-retry',
    screenshot: 'only-on-failure',
```

exercises