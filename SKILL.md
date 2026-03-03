---
name: siteconfig-maker
description: Create siteconfig files to help extract content from websites
license: MIT
compatibility: Requires access to the internet
metadata:
  author: Ansel Halliburton
---

# Siteconfig Maker

## When to use this skill

Use this skill to create siteconfig file of extraction rules for working with a website.

## About siteconfig files

Siteconfig files are small text files that contain rules for extracting information from websites. 

### Format documentation

The most comprehensive documentation of the siteconfig file format is the "Site Patterns" page of the FiveFilters.org documentation site: https://help.fivefilters.org/full-text-rss/site-patterns.html.

Additional information has been collected and published at https://github.com/digicommons/ftr-site-config-directives.

### Filename convention

A single siteconfig file typically contains has rules for one website, and its filename is the website's hostname plus a ".txt" ending. For example, the CNN news website, available at the hostname cnn.com, would have rules in a siteconfig file named "cnn.com.txt".

### Rule types

There are two predominant rule types: XPath and string.

#### XPath rules

XPath rules provide an XPath expression to locate an element in a webpage's HTML source. An example from the documentation page is:

```
title: //h1[@id='title']
```

- `title` indicates that the line states a rule for extracting the title of the webpage.
- `//h1[@id='title']` is the XPath expression that identifies the HTML element containing the title.

#### String rules

String rules match simple text strings. One example is the `strip_id_or_class` rule. The documentation page gives these examples:

```
strip_id_or_class: hidden
strip_id_or_class: navigation
```

This shows that the `strip_id_or_class` rule can be repeated. Here, HTML elements with IDs or CSS classes matching either "hidden" or "navigation" match the rule, and will be removed.

## Instructions

- For the given URL, crawl the URL and obtain its HTML source.
- Create at least the following extraction rules. If it is not possible to create at least these rules, the skill should fail with an error message saying so.
  - `title`: An XPath rule specifying the semantic title of the page, such as the title of a news article
  - `body`: An XPath rule identifying the HTML element that serves as the container of the main content, i.e., which does *not* include page-nonspecific elements like global navigation, page footers, etc.
- Additionally (but optionally) try to create these additional rules:
  - `date`: An XPath rule identifying the publication date
  - `author`: An XPath rule identifying the author, or authors, of the page
  - `strip`: A repeatable XPath rule for undesired elements.
  - `strip_id_or_class`: A repeatable string rule specifying the HTML IDs or CSS classes for undesired elements.

## Undesired elements

Try to remove the following undesired elements by using `strip` and similar rules:

- Advertisements
- Chumboxes (low-quality lists of articles from providers like Taboola, which often appear at the end of articles)
- Navigation elements
- Page headers or footers

## References

- XPath cheatsheet: https://quickref.me/xpath
- `ftr-site-config` repository of hundreds of siteconfig files contributed by community: https://github.com/fivefilters/ftr-site-config
- Online tool for creating siteconfigs: https://siteconfig.fivefilters.net/
- Test a siteconfig file with: https://f43.me/feed/test
