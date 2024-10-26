---
title: "Wrangling in Legacy Code"
date: 2023-02-04T09:54:12-06:00
draft: false
featuredimage: /posts/2023/wrangling-legacy-code-splash.jpg
---
Working with legacy code can be a challenge, but with a few best practices in place, it can become a manageable task. Over the years, I've learned a few tips that make it easier for teams to get a grip on the codebase.

1. Set up a script for the local environment. To streamline the process, use the tools that the team is most familiar with, whether it be Vagrant, Chef, Powershell DSC, or something else. The goal is to make the setup as quick and easy as possible.

1. Implement a Continuous Integration (CI) build. If your team doesn't have one yet, now is the time to set it up. Start with a basic setup and add test runners, code coverage, and static analysis tools as needed in the future. Many source control providers offer a hosted solution that allows you to set up a CI build with just a few clicks.

1. Establish clear code ownership. Assign a specific team to own each area of the codebase, and make sure they sign off on every change. This will provide a clear boundary for code changes, making it easier to maintain and update the code.

1. Break up large projects. Shared "utility" libraries that don't have a clear owner can become a dumping ground for code. It sounds like heresy but to avoid this, copy these libraries into the new projects and have each team maintain their own version. This will allow each team to trim down the code to what they need and maintain it as they see fit.

By following these steps, teams can effectively work with legacy code and make it easier for future developers to understand and maintain.
