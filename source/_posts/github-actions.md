---
title: github-actions
date: 2021-03-17 11:32:01
tags:
---
https://github.com/developit/redaxios
这个项目有.github/workflows文件

github actions:
https://docs.github.com/cn/actions/quickstart

https://docs.github.com/en/github/using-git/git-workflows

### artus workflow 配置
#### package.json
package.json + "ci"

#### .github/workflows
nodejs.yml
```
# This workflow will do a clean install of node dependencies, build the source code and run tests across different versions of node
# For more information see: https://help.github.com/actions/language-and-framework-guides/using-nodejs-with-github-actions

name: Node.js CI

on:
  push:
    branches:
      - main
      - master
  pull_request:
    branches:
      - main
      - master
  schedule:
    - cron: '0 2 * * *'

jobs:
  build:
    runs-on: ${{ matrix.os }}

    strategy:
      fail-fast: false
      matrix:
        node-version: [14, 16, 18]
        os: [ubuntu-latest, windows-latest, macos-latest]

    steps:
    - name: Checkout Git Source
      uses: actions/checkout@v2

    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}

    - name: Install Dependencies
      run: npm i

    - name: Continuous Integration
      run: npm run ci

    - name: Code Coverage
      uses: codecov/codecov-action@v1
      with:
        token: ${{ secrets.CODECOV_TOKEN }}

```