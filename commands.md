dinosaurs=# select Count(*) from dinosaurs
dinosaurs-# ;
ERROR:  relation "dinosaurs" does not exist
LINE 1: select Count(*) from dinosaurs
                             ^
dinosaurs=# select Count(*) from dinos;
 count 
-------
   331
(1 row)

dinosaurs=# select * from dinos where period='Jurassic';
dinosaurs=# select sum(length) from dinos where period='Cretaceous';
   sum   
---------
 1366.45
(1 row)

dinosaurs=# select * from dinos where period='Jurassic' or period='Cretaceous', Order by ASC;
ERROR:  syntax error at or near ","
LINE 1: ...nos where period='Jurassic' or period='Cretaceous', Order by...
                                                             ^
dinosaurs=# select * from dinos where period='Jurassic' or period='Cretaceous' Order by ASC;
ERROR:  syntax error at or near "ASC"
LINE 1: ...where period='Jurassic' or period='Cretaceous' Order by ASC;
                                                                   ^
dinosaurs=# select * from dinos where period='Jurassic' or period='Cretaceous' Order species by ASC;
ERROR:  syntax error at or near "species"
LINE 1: ...re period='Jurassic' or period='Cretaceous' Order species by...
                                                             ^
dinosaurs=# select * from dinos where period='Jurassic' or period='Cretaceous' Order by species ASC;
dinosaurs=# select * from dinos where t_order = 'Saurischia' and diet = 'Herbivorous'; 
dinosaurs=# select min(length) from dinos;
 min  
------
 0.08
(1 row)

dinosaurs=# select min(length) from dinos Rename name to Shortie;
ERROR:  syntax error at or near "name"
LINE 1: select min(length) from dinos Rename name to Shortie;
                                             ^
dinosaurs=# select min(length) from dinos Update name = 'Shortie';
ERROR:  syntax error at or near "name"
LINE 1: select min(length) from dinos Update name = 'Shortie';
                                             ^
dinosaurs=# UPDATE MainTable
dinosaurs-#    SET [Date] = GETDATE()
dinosaurs-# select min(length) from dinos Update name = 'Shortie';
ERROR:  syntax error at or near "["
LINE 2:    SET [Date] = GETDATE()
               ^
dinosaurs=# UPDATE dinos
dinosaurs-# set name = 'Shortie'
dinosaurs-# where 1 = (SELECT min(length) FROM dinos);
UPDATE 0
dinosaurs=# select * from dinos where length= 0.08;
dinosaurs=# UPDATE dinos                           
set name = 'Shortie'
where max = (SELECT min(length) max FROM dinos);
ERROR:  column "max" does not exist
LINE 3: where max = (SELECT min(length) max FROM dinos);
              ^
dinosaurs=# UPDATE dinos
set name = 'Shortie'
where length= (SELECT min(length)  FROM dinos);
UPDATE 1
dinosaurs=# select * from dinos where length= 0.08;
dinosaurs=# select min(length) from dinos
dinosaurs-# ;
 min  
------
 0.08
(1 row)

dinosaurs=# select min(length) lll from dinos;
 lll  
------
 0.08
(1 row)

dinosaurs=# select * from dinos Order by name ASC;
dinosaurs=# selec name from dinos Order by 1 ASC;
ERROR:  syntax error at or near "selec"
LINE 1: selec name from dinos Order by 1 ASC;
        ^
dinosaurs=# select name from dinos Order by 1 ASC;
dinosaurs=# select name from dinos Order by 1;