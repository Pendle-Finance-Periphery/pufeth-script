## Pendle Time-weighted Balance Sentio Indexer


### Setup

1.  Create `./sentio.yaml` file and put in `project: <YOUR_PROJECT_NAME>`.
2. Modify addresses configuration and sampling frequency in `./src/consts.ts`.

### Query


1. Get the latest updated block from the sentio using sql command: 

```sql
select max(block_number) from `updating-block`
```


2. Query time-weighted share of users from your `<PREVIOUS_BLOCK>` to `<LAST_UPDATED_BLOCK>`.

```sql
select sum(point) as share, account as user from `point_increase` 
where 
    block_number > <PREVIOUS_BLOCK> 
    and block_number <= <LAST_UPDATED_BLOCK> 
group by account
```

3. Query current holding of users:

```sql

select account as user, amountYieldTokenHolding as balance from `point_increase` 
where block_number = <LAST_UPDATED_BLOCK>
```
