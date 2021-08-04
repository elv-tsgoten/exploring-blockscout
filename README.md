# Blockscout Findings

Below are my findings for our implementation of blockscout and the available data in the db.


### Blockscout Links
This is the main DB Schema linked in Blockscout's website 
https://github.com/blockscout/docs/blob/master/.gitbook/assets/bs_db_scheme.png
https://docs.blockscout.com/for-developers/db-schema
I will refer to the tables described in this Schema and how it pertains to our implementation. 
![](https://gblobscdn.gitbook.com/assets%2F-Lq1XoWGmy8zggj_u2fM%2F-MA5flVCI-YNFUDsG334%2F-MA5iM-buMVAlzXQBq0M%2FBS_DB_scheme.png?alt=media&token=3ce78d1f-187d-41ff-84da-749fc0989c76)

### Notes
My findings are from a dump of DemoV3 on July 29, 2021. If significant changes have been made since, then this is no longer up to date. 

# Summary of Significant Tables

|Table Name  | Notes |
|--|--| 
| addresses | Has the hash primary key which is very useful. Useful for coin balance data. | 
| blocks | Hash primary key. Very useful for finding the timestamp. Also has the gas data for that block. Use `to_date(timestamp::TEXT, 'YYYY-MM-DD HH24:MI:SS')` in sql to convert time string to timestamp. |
| transactions | especially useful for looking at `from_address_hash` and `to_address_hash` which can be used as primary keys in the other tables. |
| logs | Very useful for getting the `first_topic` can be used to see very easily which events have occurred. Also works well with blocks table to find timestamp of events. 
| smart_contracts | no data :(
| users | no data :(
| tokens | useful data! Has the name of the various tokens, as well as the type (ERC-20, ERC-721) etc. 