---
layout: post
title: Duplicate a raw in SQL
date: 2020-06-13 13:51
category:
author: Prasanth Kanna
tags: [SQL]
description: How to duplicate a row inside a table in SQL
image: duplicate_a_row_sql/img.jpg
---

Let's suppose a table has 200 columns and 500 rows. It has the first column as Identity. You might want to insert a new row having the same values as the last row. What would you do? Copy the whole row and explicitly insert `,` and `'` wherever necessary and execute an Insert command? It would take a lot of time especially if the table has large number of columns like 200 in our case. The efficient and time saving solution for this problem is:

1. Insert the desired row you want to duplicate into a temporary table.
2. Do any of the following as per your requirement:
    * Drop the identity column from the temporary table(if you want to duplicate based upon identity column)
    * Update the Primary key entry(or any other columns which you might want to change) in the temporary table(if you want to duplicate based upon primary key or any other column)
3. Insert the row from temporary table into the actual table.
4. Drop the temporary table(optional but good practice)

The SQL command would look like this:

{% highlight sql %}
SELECT * INTO #temp FROM <your_table> WHERE <conditions>

-- Execute any of the below commands as per requirement --
ALTER TABLE #temp DROP COLUMN <identity_column>
                -- OR --
UPDATE #temp SET <primary_key_or_other_columns>
----------------------------------------------------------

INSERT INTO <your_table> SELECT * FROM #temp
{% endhighlight %}
