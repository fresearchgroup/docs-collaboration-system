---
id: collaborate
title: Contributing to Collaboration System
sidebar_label: Contributing to Collaboration System
---

Want to contribute? Collaborative Communities is an open source project and we welcome contributions. We would be very happy to collaborate with you. To make contributions in our project please make sure that you read this document and follow the guidelines given.

## Contributing Workflow
Collaborative Communities project is on Git and we follow the git working model. If you are new to git then try familiarizing yourself with git first. You may also refer a concise guide  (https://docs.google.com/document/d/19Rlhhp2FtZ_qboNkETuoVQ1uAgefPqWe3Yy7Rwl9IqY/edit?usp=sharing) or a detailed one (https://git-scm.com/book/en/v2)

### Fork Repository and Choose Branch
- The first step is to fork the repository so that you have your own repository on which you can work on.
- You must then identify the branch on which you would like to contribute. You are free to create a new branch in your repository but make sure that you create it from the desired working branch only.

### Contribute to a branch
- Once the branch is chosen, you can start contributing. Make sure that you follow the ‘Contributing guidelines’.
- We use Travis for continuous integration and Codefactor to check the quality of code. To ensure that there is no problem while merging your code, we recommend that you use these in your forked repository as well.
- Commit your code to your forked repository on a regular basis with meaningful commit messages. After all contributions, i.e. just before you submit your code, squash your commits into one commit. This avoids the cluttering of all the commits during merging. (https://gist.github.com/patik/b8a9dc5cd356f9f6f980)
- There might be some changes to the original repository which will not reflect in your forked repository. If you want to update it, sync it using the steps given in the link: https://help.github.com/articles/syncing-a-fork/

### Make a pull request
- When you feel that you are ready to merge your contributions into our repository, create a pull request.
- Select an appropriate label from the list E.g. enhancement, bug fix, etc.
- Each pull request should be for a single feature or addressing a single problem only. Avoid handling multiple features or bug fixes into one pull request.
- Ensure that you create it for the appropriate branch only.
- Write a brief description about your contribution and what problem does it solve. A pull request with good description is always appreciated and will be accepted easily.
- Once the pull request is made, Codefactor will check for the quality of your code and Travis will build the system. If both goes well then ‘All checks have passed’ will be displayed on your pull request. If any one fails, you can check the details.
- Our reviewing team will review your pull request and will interact with you by posting comments. You may be asked to modify incase there is any issue.

## Contributing Guidelines
- You can contribute by: (a) fixing a bug, (b) improving the UI, (c) creating a new feature, (d) updating the documentation, etc.
- Before you start contributing, first browse through the issues and pull requests to know whether someone else has already fixed the issue or is already working on the feature.
- Follow the django coding style:
https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/
- If you are modifying or adding a feature then write unit test cases as well.
- Avoid unnecessary modification of existing code. Ofcourse, you are free to optimize and resolve bugs.
- Avoid duplication of code
- Break your code/logic into different functions and add comments for better understanding.
- If your contributions have some dependencies or they modify existing structure, then update the README.md file accordingly. Also feel free to add more documentation files.
