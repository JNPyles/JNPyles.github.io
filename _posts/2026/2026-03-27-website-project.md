---
title: "Personal Website"
date: 2026-03-27
tags: [Project]
github_url: "https://github.com/JNPyles/JNPyles.github.io"
---

## Overview
The primary purpose of **jnpyles.com** is to serve as a centralized, permanent home for my technical projects and professional insights.

## Tech Stack & Architecture
The site is built with a focus on speed, security, and maintainability. By using a static site generator, I can ensure fast load times and a simple deployment workflow.

* **Framework:** [Jekyll](https://jekyllrb.com/) (Static Site Generator)
* **Hosting:** [GitHub Pages](https://pages.github.com/)
* **Templating:** Liquid
* **Content:** Markdown & YAML Front Matter
* **DNS & Security:** Custom domain integration with restrictive SPF, DKIM, and DMARC records to prevent email spoofing.

## The Build Process
The architecture follows a "Docs-as-Code" philosophy. Every post and project page is written in Markdown and tracked via version control in my [GitHub repository](https://github.com/JNPyles/JNPyles.github.io). 

One of the key features of the build is the automated categorization system. Using **Liquid loops**, the site dynamically generates an "Articles" page and a "Projects" page, grouping content based on metadata defined in each file's front matter. This allows for a scalable content structure where adding a new project is as simple as dropping a Markdown file into the repository.

## Lessons Learned
Building this site reinforced the importance of clean DNS management and the power of static site generators. Transitioning from social-media-first content to a self-hosted model has provided better control over how technical information is presented and preserved.
---