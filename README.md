Advance Database Organization
=============================

This repository contains all the class projects related to the course "Advance Database Organization".

If I were to give the gist of this course then I learnt how to develope a basic SQL database manager. Management of resources like primary and secondary memore while storing and retrieving the data from a table.

I learnt this in 4 stages each stage based on top the previous. Thus the 4 projects which are described bellow. 


# Storage Manager
'''
Storage manager is an application which handles Create, Open, Close, Destroy and all the read/write
funtionalities to the files that are stored on the disk.
This is the basic building block for the final application. This part of the application defined methods that handles the basic read/write of a binary file. 
This manager keeps track of the number of pages and content each page. Each page stores part or the entire table 
'''

# Buffer Manager
'''
This manager is built upon the previous manager. This wraps the pages suplied by the previous manager into blocks. Each block can consist of many pages. This block is referred to as *PAGE FRAMES* in this file.
Now the functionality of this manager is handling the swaping of *Page Frames* in and out of primary memory from the secondary memory.
There are 2 basic page replacement strategies implemented in this manager.
* FIFO - First In First Out
* LRU - Least Recently Used
'''

# Record Manager

This manager is again built on the foundation formed by the previous 2 managers. This manager introduce tables and records. Each table will be defined with a certain schema. This inturn defines the structure of each record. A record can be looked at as a row in a table.
So this manager defines the methods that enable the user to operate on tables.
The records 


# B+ Tree Page Buffer Manager

This is built on the buffer and page manager. This manager is an optimization solution to smartly index the pages. By doing so we can reduce the access time to a super logarithmic scale. 


## Detailed information on each manager is provided in the individual sub folders
