

### 1. Read Committed: No dirty reads


#### EXPERIMENT

**user2>** 

- sql command(s) ...
- command output (if any) ...

**user1>** 

...

**user2>** 

...

**user1>** 

...

**user2>** 

...


#### FINDINGS

User2 doesn't see the value set by User1's uncommited transaction.  
User2 sees the updated value when the transaction has been commited.

(... for example ...)


### 2. Read Committed: No dirty write - automatically started transactions


#### EXPERIMENT

**alice>**

...

**bob>**

...

**alice>**

...

**Result**

```sql
select listings.id, listings.buyer, invoices.recipient
from listings join invoices on listings.id = invoices.listing_id
where listings.id =  1234;
```

...


#### FINDINGS

...



### 3. Read Committed: No dirty write - manually started transactions


#### EXPERIMENT

**alice>**

...

**bob>**

...

**alice>**

...

**Result**

```sql
select listings.id, listings.buyer, invoices.recipient
from listings join invoices on listings.id = invoices.listing_id
where listings.id =  1234;
```

...


#### FINDINGS

...



### 4. Repeatable read - automatically started transactions


#### EXPERIMENT

**alice>**

...

**transfer>**

...

**alice>**

...


#### FINDINGS

...


### 5. Repeatable read - manually started transactions


#### EXPERIMENT

**alice>**

...

**transfer>**

...

**alice>**

...


#### FINDINGS

...


### 6. Repeatable read - manually started transactions, journal_mode=WAL


#### EXPERIMENT

**alice>**

...

**transfer>**

...

**alice>**

...


#### FINDINGS

...


### 7. Preventing Lost Updates: Atomic write operations


#### EXPERIMENT

**user1>**

...

**user2>**

...

**Result**

```sql
 select * from t;
```

...


#### FINDINGS

...


### 8. Preventing Lost Updates: Compare and set


#### EXPERIMENT

**user1>**

...

**user2>**

...

**user1>**

...

**user2>**

...

**Result**

```sql
select * from t where key = 'counter';
```

...


#### FINDINGS

...

