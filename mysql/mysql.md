
## mysql 执行顺序
SELECT DISTINCT <select_list>
FROM <left_table>
<join_type> JOIN <right_table>
ON <join_condition>
WHERE <where_condition>
GROUP BY <group_by_list>
HAVING <having_condition>
ORDER BY <order_by_condition>
LIMIT <limit_number>

## where 和 having 区别  
where： 用来约束来自数据库的原始数据，数据库中原始没有的 不能用where  
having: 对查询后的结果集进行过滤（一般用来过滤聚合函数结果集）

``` sql 
select region,sum(population),sum(area) from bbc group by region;

select region,sum(population),sum(area) from bbc group by region having sum(population) > 1000000;
```

## distinct 和 group by  
distinct只是将重复的行从结果中出去；
group by是按指定的列分组，一般这时在select中会用到聚合函数也可不用  
group by 效率明显比 distinct 高