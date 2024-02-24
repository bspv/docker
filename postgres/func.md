### postgres函数语法

##### 1.打印输出
```
RAISE NOTICE '参数1 ： % ，参数2： %',param1,param2;
```

##### 2.赋值
```
1).直接赋值
param_year := 2024;

2).从调用参数中获取值进行赋值
p_date_column_name := TG_ARGV[0];

3).获取对应字段的值
EXECUTE 'SELECT $1.'||p_date_column_name INTO curYMD USING NEW;

4).查询结果赋值
SELECT count(*) INTO existTaskId FROM information_schema.columns WHERE table_schema=curSchema AND table_name=tableNames[i] AND column_name = 'p_taskid';

5).使用ARRAY_AGG函数将查询的某一列转成数组赋值
SELECT ARRAY_AGG(table_name::text) INTO tableNames FROM information_schema.tables WHERE table_schema = current_schema();
```

##### 3.获取内置函数值
```
current_schema() //当前模式

information_schema.tables //所有表信息，可以查询所有表
information_schema.columns //所以列信息，可以查询某个表是否有某个字段对应列
```

##### 4.数组
```
1).一维数组定义
start_idx_arr := ARRAY[1,11,21];

2).二维数组定义，元素数量必须相等
province_code_arr := ARRAY[
  [-1,110000,120000,310000,500000,810000,820000,990000],
  [-2,650000,530000,450000,520000,360000,320000,330000],
  [-3,540000,620000,430000,440000,410000,350000,640000],
  [-4,150000,230000,610000,420000,370000,340000,460000],
  [-5,630000,510000,220000,130000,140000,210000,710000]
];

3).获取数组长度
array_length(province_code_arr, 1)//1代表维度，如果二维数组也可以用2获取内层一维数组长度
```

##### 5.IF条件判断
```
1).普通IF
IF (tableNames[i] ~ '2') = false THEN
  RAISE NOTICE 'tableNames[i]对应字符串不含有2';
END IF;

2).IF-ELSEIF-ELSE
IF param_month < 4 THEN
  squarter := param_year||'-Q1';
ELSEIF param_month < 7 THEN
  squarter := param_year||'-Q2';
ELSEIF param_month < 10 THEN
  squarter := param_year||'-Q3';
ELSE
  squarter := param_year||'-Q4';
END IF;

```

##### 6.FOR循环
```
FOR k IN 1..array_length(start_idx_arr, 1) LOOP
  RAISE NOTICE '元素： % = %',k,start_idx_arr[k];
END LOOP;
```

##### 7.FORMAT格式化
```
format('CREATE TABLE %s.%s PARTITION OF %s.%s FOR VALUES FROM (%L) TO (%L)', curSchema,partitionTableName,curSchema,tableNames[i],startTime,endTime);

%s : s将参数值格式化为一个简单字符串
%I : I将参数值视作 SQL 标识符，并在必要时用双写引号包围它。如果参数为空，将会是一个错误
%L : L将参数值引用为 SQL 文字。一个空值将被显示为不带引号的字符串NULL
```

##### 8.EXECUTE执行
```
EXECUTE 'SELECT $1.'||p_date_column_name INTO curYMD USING NEW; //执行 `字符串`
```

##### 9.to_char函数
```
curYMD := '20240101';
startTime := to_char(curYMD::timestamp, 'YYYY-MM-DD');//2024-01-01
endTime := to_char( startTime::timestamp + interval '1 day', 'YYYY-MM-DD');//2024-01-02 , + interval '1 day'是往后加1天
```

##### 10.replace函数
```
replace(curTaskId, '-', ''); //第二个参数为要替换的值，第三个为替换值
```

##### 11.GREATEST函数
```
GREATEST(province_code_arr[j], 0); //获取两个参数中的较大值
```