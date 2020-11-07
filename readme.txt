# dbms_miniProject_online-shopping
Contribution : MD Aawesh Patanwala(111803146)
               Shrijeet Ramteke(111803140)

Hosted on Github : https://github.com/aawesh2000/dbms_miniProject_online-shopping
=========================================================================================================================================================								
About the project:-
	This is an online-shopping system, created using MySql Database,PHP,HTML,CSS. This project will give the user an insight
about the real world online-shopping system like Amazon,Flipkart etc. The user can Shop Electronics,Clothes and other accessories
as well as he/she can also enjoy the discount facility. The user will need to register firstly to login next time. This system will 
also help you by suggesting top deals. The payment facility has also been included such that he/she will find ease in placing the order.
=========================================================================================================================================================			Frontend Used :- HTML,CSS
Backend Used :- PHP
=========================================================================================================================================================		
Features

1)Provide stastic analysis to customer and sellers.
2)For customers provide analysis of spending over various categories.
3)For sellers provide analysis of sell ratio over various cities.

=========================================================================================================================================================								
RELATIONAL SCHEMA :-
admin_info : pk:admin_id							Functional Dependency:
										admin_id->admin_name
  `admin_id` int(10) NOT NULL,							admin_id->admin_email
  `admin_name` varchar(100) NOT NULL,						admin_id->admin_password
  `admin_email` varchar(300) NOT NULL,
  `admin_password` varchar(300) NOT NULL

Already in 1NF 
Already in 2NF
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
brands : pk : brand_id								Functional Dependency:
`brand_id` int(100) NOT NULL,							brand_id->brand_title
`brand_title` text NOT NULL

Already in 1NF
Already in 2NF
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
Cart: pk: id									Functional Dependency:
  `id` int(10) NOT NULL,							id->p-id
  `p_id` int(10) NOT NULL,							id->user_id
  `user_id` int(10) DEFAULT NULL,						id->quantity
  `qty` int(10) NOT NULL

Already in 1NF

Since the p_id(Product_id) can take similar value(depending on the category of the product like electronics,home appliances etc) it is necessary to split the table into two, Giving us 2nd Normal Form

		Table1:   											Table2:
   		id													   id
	       user_id												   p_id
  	       qty
 
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
categories: pk:cat_id								Functional Dependency:
`cat_id` int(100) NOT NULL,							cat_id->cat_title
`cat_title` text NOT NULL

Already in 1NF
Already in 2NF
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
email info: pk:email_id								Functional Dependency:
`email_id` int(100) NOT NULL,							email_id->email
`email` text NOT NULL

Already in 1NF
Already in 2NF
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
orders: pk : order_id 								Functional Dependency:
`order_id` int(11) NOT NULL,							order_id->user_id
`user_id` int(11) NOT NULL,							order_id->product_id
`product_id` int(11) NOT NULL,							
`qty` int(11) NOT NULL,
`trx_id` varchar(255) NOT NULL,
`p_status` varchar(20) NOT NULL

Already in 1NF
As a user can order more than 1 products, the product_id column will contain more than two values, Hence we need to spilt it into different  tables and we get the 2nd Normal Form with  single column Primary  key i.e order_id.

		Table1 :													Table 2:
		order_id													order_id
		user_id													product_id
		qty
		trx_id	
		p_status

If there is a change in in user_id the transaction id p_status and order_id will change, hence we should split it into different column and remove the Transitive Dependency. This gives us 3rd Normal Form.

	Table1:								Table2:								Table3:
	order_id								order_id								order_id
	qty									product_id							user_id
	trx_id
	p_status

---------------------------------------------------------------------------------------------------------------------------------------------------------

orders_info: pk:order_id, user_id							Functional Dependency:
`order_id` int(10) NOT NULL,								order_id->user_id
`user_id` int(11) NOT NULL,								user_id->f_name
`f_name` varchar(255) NOT NULL,								user_id->email
`email` varchar(255) NOT NULL,								user_id->address
`address` varchar(255) NOT NULL,							user_id->city
`city` varchar(255) NOT NULL,								user_id->state
`state` varchar(255) NOT NULL,								user_id->zip
`zip` int(10) NOT NULL,									
`cardname` varchar(255) NOT NULL,
`cardnumber` varchar(20) NOT NULL,
`expdate` varchar(255) NOT NULL,
`prod_count` int(15) DEFAULT NULL,
`total_amt` int(15) DEFAULT NULL,
`cvv` int(5) NOT NULL

Already in 1NF
Already in 2NF  since in it each column will have only one value
Now the attributes, address, city, state, zip for a user can be same. Here comes the Transitive Dependency of the table. Hence to remove it we split it into two different  tables. This gives us 3rd Normal Form.

			Table1:												Table2:
			order_id												user_id
			user_id												f_name
			cardname											email
			cardnumber											address
			expdate												city
			prod_count											state	
			total_amt											zip
			cvv
			

---------------------------------------------------------------------------------------------------------------------------------------------------------
orders_products: pk:order_pro_id, order_id, product_id				Functional Dependency:
`order_pro_id` int(10) NOT NULL,						order_pro_id->order_id
`order_id` int(11) NOT NULL,
`product_id` int(11) NOT NULL,
`qty` int(15) DEFAULT NULL,
`amt` int(15) DEFAULT NULL

Already in 1NF
Already in 2NF
Now here if the user want's to change his product quantity, the  amount quantity will also change depending on it hence the Transitive Dependency must act and change should take place. Hence we keep it in same table only.
Already in 3NF
---------------------------------------------------------------------------------------------------------------------------------------------------------
products: pk:product_id 							Functional Dependency:
  `product_id` int(100) NOT NULL,						product_id->product_brand
  `product_cat` int(100) NOT NULL,
  `product_brand` int(100) NOT NULL,
  `product_title` varchar(255) NOT NULL,
  `product_price` int(100) NOT NULL,
  `product_desc` text NOT NULL,
  `product_image` text NOT NULL,
  `product_keywords` text NOT NULL

Already in 1NF
The product_image can have the column repeated. Hence it is necessary to split it into different table to give single column primary key. Hence we get 2nd Normal Form.
			Table1:												Table2:
			product_id											product_id
			product_cat											product_image
			product_brand
			product_title
			product_price
			product_desc
			product_keywords
			
For 3rd Normal form, we remove Transitive Dependency.
		Table1:							Table2:						Table3:
		product_id						product_id					product_id
		product_cat						product_image				product_title
		product_brand												product_price
																	product_desc
																	product_keywords

---------------------------------------------------------------------------------------------------------------------------------------------------------
user_info: pk: user_id
  `user_id` int(10) NOT NULL,
  `first_name` varchar(100) NOT NULL,
  `last_name` varchar(100) NOT NULL,
  `email` varchar(300) NOT NULL,
  `password` varchar(300) NOT NULL,
  `mobile` varchar(10) NOT NULL,
  `address1` varchar(300) NOT NULL,
  `address2` varchar(11) NOT NULL

Already in 1NF
As address and mobile number can take  multiple value, we split it into different tables to get 2NF.
				Table1:												Table2:
				user_id												user_id
				first_name											mobile
				last_name											address1
				email												address2
				password

As there is no Tansitive Dependency we can say it is already in 3NF.
---------------------------------------------------------------------------------------------------------------------------------------------------------
user_info_backup: pk:user_id
`user_id` int(10) NOT NULL,
  `first_name` varchar(100) NOT NULL,
  `last_name` varchar(100) NOT NULL,
  `email` varchar(300) NOT NULL,
  `password` varchar(300) NOT NULL,
  `mobile` varchar(10) NOT NULL,
  `address1` varchar(300) NOT NULL,
  `address2` varchar(11) NOT NULL


Already in 1NF
As address and mobile number can take  multiple value, we split it into different tables to get 2NF.
				Table1:												Table2:
				user_id												user_id
				first_name											mobile
				last_name											address1
				email												address2
				password

As there is no Tansitive Dependency we can say it is already in 3NF.

--------------------------------------------------------------------------------------------------------------------------------------------------------

Installation and Running : 
You need to install XAMPP and on apache & sql server
and save this project at C Drive->xampp->htdocs->paste the project
now, type->http://localhost/online-shopping-system-master and hit enter


