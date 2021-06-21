---
title: "MySQL notes"
date: 2021-06-18T19:28:02+08:00
draft: false
tags: ["MySQL"]
---

# MySQL Utilities Console

## db export
```sh
mysqldbexport --server={user}:{password}@{server.domain.com}:3306 {db_name} --output-file={dump_ge.sql}
```