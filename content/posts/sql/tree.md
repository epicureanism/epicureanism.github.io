---
title: "A Table with Adjacency List structure"
date: 2021-06-21T19:28:02+08:00
draft: true
tags: ["SQL"]
---
# Tables with Adjacency List 
Inspired by the adjacency list of [Models for hierarchical data][slides]

## To show the depth, id concatenation, and sum up of the tree
```sql
with recursive tree (id, agent_id, account, depth, path, id_as_path, deposit_sum) as (
  select u.id, u.agent_id, u.account, 1 as depth, cast(u.account as char(200)) as path, cast(u.id as char(200)) as id_as_path
		, s.debit_sum as deposit_sum
  from user u left join vw_user_deposit_stat s on u.id = s.user_id			
  where      agent_id is null 
  union all
  select u.id, u.agent_id, u.account, tree.depth + 1 as depth, CONCAT(tree.path, ',', u.account) as path, CONCAT(tree.id_as_path, ',', u.id) as id_as_path
		, s.debit_sum as deposit_sum
  from user u inner join tree on u.agent_id = tree.id
			  left join vw_user_deposit_stat s on u.id = s.user_id
)
select *
from tree
```

# Ref
- [Models for hierarchical data][slides]
  
  [slides]: https://www.slideshare.net/billkarwin/models-for-hierarchical-data        "Models for hierarchical data"