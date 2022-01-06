---
title: Doing a table join in Android without using rawQuery
slug: doing-a-table-join-in-android-without-using-rawquery
date_published: 2015-12-30T00:00:00.000Z
date_updated: 2018-04-16T16:13:05.000Z
---

Android has some really nice SQLite helper classes and methods. And the ones I like the most are the *SQLiteDatabase.query*, *SQLiteDatabase.update*, *SQLiteDatabase.insert* ones, because they take away quite a bit of pain for typing out SQL commands by hand.

But unfortunately, if you have to use a JOIN, then usually you have to go and use the *SQLiteDatabase.rawQuery* method and end up having to type your commands by hand.

But but but, if the two tables you are joining do not have any common column names (actually it is good design to have them so - by having all column names prefixed by `tablename_` maybe), then you can hack the usual `SQLiteDatabase.query()` method to get a JOINed query.

See the two tables I have here -

> A bit of context - this is an app about tracking car expenses and refuels.
> 
> Refuels/Services/etc are all various types of expenses.
> 
> So the 'expense' table has all expenses. The 'refuel' table has all refuels
> 
> and a reference to corresponding expense entries (one to one).

Expense table
![Expense](/content/images/2018/04/andtbl1.png)

Refuels table
![Refuel](/content/images/2018/04/andtbl2.png)

Where `exp_id` is a foreign key referencing `expense_id`

Now ideally, to get the expense where refuel_id was **1**, a nice looking SQL query should be like this -

    SELECT * FROM expense INNER JOIN refuel
    ON exp_id = expense_id
    WHERE refuel_id = 1
    

Which, in android, can be done like this -

    String rawQuery = "SELECT * FROM " + RefuelTable.TABLE_NAME + " INNER JOIN " + ExpenseTable.TABLE_NAME
            + " ON " + RefuelTable.EXP_ID + " = " + ExpenseTable.ID
            + " WHERE " + RefuelTable.ID + " = " +  id;
    Cursor c = db.rawQuery(
            rawQuery,
            null
    );
    

But of course, because of SQLite's backward compatible support of the primitive way of querying, we turn that command into

    SELECT *
    FROM expense, refuel
    WHERE exp_id = expense_id AND refuel_id = 1
    

Now this we can write by hacking the terminology used by the #query() method -

    Cursor c = db.query(
            RefuelTable.TABLE_NAME + " , " + ExpenseTable.TABLE_NAME,
            Utils.concat(RefuelTable.PROJECTION, ExpenseTable.PROJECTION),
            RefuelTable.EXP_ID + " = " + ExpenseTable.ID + " AND " + RefuelTable.ID + " = " +  id,
            null,
            null,
            null,
            null
    );
    

To explain a bit, the first argument `String tableName` can take `table1, table2` as well safely,

The second argument takes a String array of column names, I concatenated the two projections of the two classes.

and finally, put by WHERE clause into the `String selection` argument.
