---
date: "2013-07-05"
title: An alternative for SQL pagination
type: post
---

I was reading up on improving the performance on MySQL when I found an article and stumbled on a really cool alternative to using offset when generating pagination results from the database.

> On the query side, instead of using `LIMIT` with `offset`, you can select one more row than you need, and when the user clicks the "next page" link, you can designate that final row as the starting point for the next set of results. For example, if the user viewed a page with rows 101 through 120, you would select row 121 as well; to render the next page, you'd query the server for rows greater than or equal to 121, limit 21.

Source: <http://www.infoworld.com/d/data-management/10-essential-performance-tips-mysql-192815?page=0,1>
