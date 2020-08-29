# Eretail
 E Commerce based project-marketplace ,orders,inventory analytics
Domain: Ecommerce
Client - Redtape, Fabindia, Lavie bags,Manyavar,Nykaa etc
Role: product specialist
Technology: SAS/SQL, Base SAS

Overview of the project: A SaaS based retail suite for MULTI CHANNEL RETAILING. It is a software product equipped with e-commerce modules Warehouse
Management System (WMS), Order Management System (OMS), Inventory Management System. It is integrated with  different marketplaces and  Transporters. 
E-Retail manages several warehouses and their operations like shipping of goods in warehouse, maintaining records of exported, imported goods etc.
We design multiple reports and real time record tracking details for Clients enabling them to strategize their Finance and Operation decisions. 

Role Description:
•	Interacting with clients to understand their requirement and designing solutions accordingly.
•	Writing codes to generate reports using Base SAS and SQL in different formats and doing Analysis based on these reports.


####
CODE-

/*sitecode wise count*/

proc sql;
create table ordercountgrph  as select sitecode ,count (*) as count from sasuser.orders;
quit;


proc gchart
data =work.ordercountgrph;
vbar sitecode/sumvar=count;
title "sitecodewise count";
run;


/*date wise count*/

proc sql;
create table ordercountgrph1  as select orderdate ,count (*) as count from sasuser.orders;
quit;


proc gchart
data =work.ordercountgrph1;
vbar orderdate/sumvar=count;
title "datewise count";
run;

/*skuwise orderqty* method to find out top sku selling/

proc sql;
 select skucode,orderqty ,count(*) as count from sasuser.obdetails group by skucode ;
quit;


##

warehouse frod detection-
total shipped qty skuwise compare with total inbound qty skuwise


## JOIN:-

/*Cartesian product*/---orders & orderdetail


proc sql obs=10;
create table cartesian_pro as select * from sasuser.orderdetail,sasuser.obdetails;
quit;


proc sql obs=10;
create table cartesian_pro1 as select orderdetail.orderno,obdetails.skucode as skuu from sasuser.orderdetail,sasuser.obdetails;
quit;


/*INNER JOIN*/


proc sql;
create table inner_jn1 as select orderinvoice.orderno,obtaxdetail.trackingno from sasuser.orderinvoice,sasuser.obtaxdetail;
quit;



proc sql;
create table inner_jn11 as select orderinvoice.orderno,obtaxdetail.trackingno from sasuser.orderinvoice,sasuser.obtaxdetail
where orderinvoice.orderno=obtaxdetail.orderno;
quit;

=

proc sql;
create table inner_jn111 as select orderinvoice.orderno,obtaxdetail.trackingno from sasuser.orderinvoice inner join sasuser.obtaxdetail
on orderinvoice.orderno=obtaxdetail.orderno;
quit;



DIFF OUTPUT why?



/*left join*/

data cards;
input cc name $;
cards;
1 A
2 B
3 C
4 D
5 E

;
run;
 data transaction;
 input cc merchant $ amount;
 cards;
 1 nike 100
 2 puma 100
 2 bb 200
 2 br 500
 4 bb 900
 4 bb 600
 ;
 run;


 proc sql;
 select a.cc ,sum(amount) as total format=dollar8.2
 from cards a left join transaction b
 on a.cc=b.cc
 group by a.cc;
 quit;



/*right join*/

data cards;
input cc name $;
cards;
1 A
2 B
3 C
4 D
5 E

;
run;
 data transaction;
 input cc merchant $ amount;
 cards;
 1 nike 100
 2 puma 100
 2 bb 200
 2 br 500
 4 bb 900
 4 bb 600
 ;
 run;


 proc sql;
select * from cards right join transaction
on cards.cc=transaction.cc;
quit;

proc sql;
select transaction.*,cards.name from cards right join transaction
on cards.cc=transaction.cc;
quit;

SAME OUTPUT

proc sql;
select transaction.*,cards.name from cards ,transaction
WHERE cards.cc=transaction.cc;
quit;



FULL JOIN:-
data a;
input id name $;
cards;
1 A
2 B
;
run;

data b;
input id sal $;
cards;
1 100
7 200
;
run;


proc sql;
select a.* ,sal from a full join b
on a.id=b.id;
quit;




####MACRO_


Ques: Create a macro which can- A) Create report in any format 
B) Create any dataset
C) From any dataset 
D) Keep any variables
E) Sort the data by any of the variable that we keep (orderinvoice)


%macro report(o=,d=,l=,k=,v=);
ods &o file="C:\Documents and Settings\sasadm\My Documents\sas codes\shivi.&o";
proc sql;
create table &d as select * from &l(keep=&k)  order by &v;
select * from &d; 
quit; 
ods &o close;
%mend report;


%report(o=pdf,d=abhay47,l=sasuser.admit,k=id name age,v=age);





ERETAIL SCRIPT:-

I am responsible for generating reports of sales order ,
purchase order,sto order and inventory ,according to client requirement.
It is like warehouse wise and marketplace wise report.

we do this activity weekely,monthly,quaterly and yearly.

sales report
inventory report
po report
sto report
return order report
Transporter-order transporter wise


and some adhoc reports also.(like how many bom sku with the child sku etc).

our db team used to feed the data in our Sas system after that we start
writing codes and creating reports.

1.First we sanitize the data to check that we are analysing the correct data
  like removing duplicates using nodupkey and nodup
  and handling missing values(NMISS,missover) as per client suggestion.


2.Then we starts coding to generate reports as per client given req.

3.After that if dashboaring is required then we send it to our other team
  to create dashboard they generate the dashboard through POWER BI and send 
  it to client.

##EXTRA POINT

1.I also review the work produced by our peer before deliver it  to the client. 

2.As an analyst ,i continue to acquire and enhance technical and nontechincal
  skills by closely working with our peer and using any available oppurtnity for that.

  Recently i have automated a major portion of our reporting by creating
  macro by which we were able to save lots of effort spend on repetative work.




