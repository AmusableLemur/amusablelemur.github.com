---
date: "2020-04-20 11:42"
title: "Creating a new user on MySQL"
type: "post"
---

Creating a new user should be a lot simpler than it is. I always forget one or two things and need to look up the exact syntax whenever I need this to make sure that everything is included properly.

This is the full command used to create a new superuser in one line with full access to all tables and ability to create new users as well. The following command essentially creates a new root user that is allowed to connect from any host so use this with caution.

    GRANT ALL ON *.* TO 'username'@'%' IDENTIFIED BY 'password' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
