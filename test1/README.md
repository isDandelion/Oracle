# Oracle
# 实验一：分析SQL执行计划，执行SQL语句的优化指导

## 实验内容：
- 对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
- 首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
- 设计自己的查询语句，并作相应的分析，查询语句不能太简单。

## 教材中的查询语句

- 查询1：

```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
#### 优化详情
![qq](https://github.com/isDandelion/Oracle/blob/master/test1/1.png)

- 查询2：
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```

#### 优化详情

![qq](https://github.com/isDandelion/Oracle/blob/master/test1/2.png)

比较：我认为下一条语句更好，用having在返回结果之后起作用更省资源



- 自定义
```SQL
select j.job_id,j.job_title 
from hr.jobs j 
where j.min_salary>3000 
order by j.job_id
```
结果

![qq](https://github.com/isDandelion/Oracle/blob/master/test1/3.png)
