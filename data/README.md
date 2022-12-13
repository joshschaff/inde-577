# Rice Bike Transaction Dataset


## What is Rice Bikes?

Rice Bikes is a student run and operated full-service bike located at the heart of Rice University's campus. They offer bike sales, rentals, and repairs targetted towards students and the greater Rice community. 

The service flow for repairs can be modelled as follows:

 - Customers make appointments online or walk in with their bike
 - A Rice Bikes mechanic completes a full diagnosis of their bike and identifies any repairs that need to be made
 - The customer and mechanic agree on what repair services are to be rendered, and the mechanic enters these repairs into our self developed app and transaction database
 - If repairs can feasibly be completed that same day or duing the original appointment slot, the mechanic will attempt to do so
 - If not, the bike goes onto the end of our repair queue
 - Bikes needing repairs are generally taken off the queue and repaired according to a "first-in first-out" (FIFO) rule

Colloquially, we refer to these same-day repairs as **"outpatient"** transactions, while those pushed onto the repair queue are known as **"inpatient"** transactions. Of particular interest to Rice Bikes is the prevalence and requisites for outpatient transactions, as they provide a better service to our customers and reduce the strain on our limited physical capacity.


## What is the data?

Each row of the dataset represents a unique transaction. There are approximately 2500 transactions spanning Fall 2021- Fall 2022. 


## What features are available?

There are over 80 features available in the dataset. The following are applicable to the notebooks in this repo:

 - **TransactionID** is a unique integer identifier for each transaction. It may be used as the row index of a dataframe
 - **TransactionType** is a categorial data value set by a mechanic at the time of transaction creation. It represents a "best guess" at what type of transaction it might turn out to be, and thus might be inaccurate by the time a transaction is completed. Valid values are
   - inpatient
   - outpatient
   - merch
   - retrospec
 - **TurnaroundTime** is the difference between when a transaction was created, and when all repairs were marked as completed. Note that it is measured in *fractinonal shifts*, where the average shift is approximately 2.5 hours, and there are on average 19 distinct shifts a week.
 - **QueueBikes** is the length of the current inpatient repair queue, mesured in integer bikes
 - **QueueRepairs** is the sum of the RepairCost for all transactions currently in the inpatient repair queue
 - **RepairCost** is the cumulative pretax cost of repairs assigned to a transaction in whole dollars
 - **PartCost** is the cumulative pretax cost of parts assigned to a transaction
 - **TotalCost** is the sum of RepairCost + PartCost
 - **DayCreated** is an integer day of the year in range [0,1,2,..,364] denoting the day when a transaction was created
 - **DayCompleted** is an integer day of the year in range [0,1,2,..,364] denoting the day when all of the repairs associated with a transaction were marked as complete
 - All remaining columns are repair counts
   - Rice Bikes' transaction database currently has 70 distinct repairs. As this is a human curated list, some repairs overlap
   - Each value in a repair count column is an integer count of the quantity of that repair which is assigned to that transaction