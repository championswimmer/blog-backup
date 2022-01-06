---
title: Change the permalink format in Ghost
slug: change-the-permalink-format-in-ghost
date_published: 2018-04-16T15:55:40.000Z
date_updated: 2018-04-16T15:55:40.000Z
---

While I am loving Ghost a lot, one thing I feel amiss is not allowing people to access all the different ways permalinks can be set. *Wordpress* allows full customisation for this.

Even on Ghost you can completely change the permalink structure, but you'll have to edit the database a bit for that.

First login to the database (if it is MySQL)

    mysql -u ghost -p 
    

(You'll find the password in your `ghost.config.json`)

Go to the table and find what your current permalink structure is like

    use ghost_production;
    select id, `key`, value from settings where `key`='permalinks';
    

![Screen-Shot-2018-04-16-at-9.22.20-PM](/content/images/2018/04/Screen-Shot-2018-04-16-at-9.22.20-PM.png)

Update it to whatever format you like

Then restart Ghost

    sudo service ghost restart
    
