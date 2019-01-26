1.一道SQL语句面试题，关于group by
表内容：
2005-05-09 胜
2005-05-09 胜
2005-05-09 负
2005-05-09 负
2005-05-10 胜
2005-05-10 负
2005-05-10 负

如果要生成下列结果, 该如何写sql语句?

            胜 负
2005-05-09 2 2
2005-05-10 1 2
------------------------------------------

create table record (date varchar(10),  status nchar(1))

insert into record values('2005-05-09','胜')
insert into record values('2005-05-09','胜')
insert into record values('2005-05-09','负')
insert into record values('2005-05-09','负')
insert into record values('2005-05-10','胜')
insert into record values('2005-05-10','负')
insert into record values('2005-05-10','负')

1)select date, sum(case when status='胜' then 1 else 0 end) '胜',sum(case when status='负' then 1 else 0 end) '负' from record group by date
2) select N.status, N.win, M.fail from 
(select date, count(*) as win from record where status='胜' group by date) N 
inner join
(select date, count(*) as fail from #tmp where status='负' group by date) M 
on N.date=M.date;


