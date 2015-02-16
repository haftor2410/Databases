# Databases

The	Project	
Write	SQL	commands	according	to	the	following	description.		
1. Create	a	view	AllAccountRecords	that	joins	the	Accounts	and	
AccountRecords	and	shows	one	entry	for	each	record	for	each	account.
The	view	should	show	all	columns	from	both	tables in	the	creation order,	
first	Accounts	and	then	AccountRecords,	except	the	AccountRecords.AID	
column. Accounts	with	no	entry	in	AccountRecords	should	be	shown with	
NULLs	in	the	columns	for	AccountRecords;	this	can	be	done	using	an	
outer	join.
2. Create	a	view	DebtorStatus	that	shows	for	each	person	who	is	in	debt	on	
at	least	one	of	their	accounts (aBalance	<	0),	the	PID	and	pName	of	the	
person,	and	the	total	amount	of	all	their	accounts.
3. Create	a	view	FinancialStatus	that	shows,	for	each	person that	has	an	
account,	the	PID	and	pName	of	the	person,	and	the	total	amount	they	have	
on	their	accounts	minus	all	unpaid	bills	that	are	past	due	date.
4. Create	a	trigger	on	the	AccountRecords table	to	a)	check	whether	the	
amount	is	available	(taking	the	overdraft	into	account)	on	any	account	
being	withdrawn	from,	b)	update	the	balance	on	the	account and	c)	install	
the	correct	balance	into	the	AccountRecords	entry.		Please	see	a	note	
below on	restrictions	on	AccountRecords.
5. Create	a	trigger	CheckBills	on	Bills	that	enforces	a)	the	rule	that	bills	
cannot	have	a	negative	amount,	and	b)	that	the	due	date	must	be	in	the	
future.
6. Create	a	trigger	CheckPeople	on	the	People	table	to	ensure	that	for	each	
new	person	a)	the	person	can	only	be	of	'M'	or	'F'	gender,	and b)	the	
height	is	not	a	negative	number.
7. Create	a	procedure	PayAllBills	that	takes	one	parameter, pPID, and	pays	
each	unpaid	bill	of	the	person	pPID	that	is	past	due	date.	The	payments	
should	come	from	the	account	with	the	highest	balance	(including	the	
overdraft)	of	the	person’s	accounts (if	two	accounts	have	the	same	
balance+overdraft,	either	one	can	chosen).	This	should	be	done	in	a	single	
transaction;	if	there	are	insufficient	funds	in	a	single	account	(including	
the	overdraft)	to	pay	all	the	bills,	then	the	operation	should	be	aborted.
The	bills	can	either	be	paid	using	a	single	AccountRecord	entry
(recommended),	or	using	multiple	AccountRecord	entries.
8. Create	a	procedure	RefundBill, that	takes	in	one	parameter,	rBID.	If	that	
bill	is	already	paid,	it	refunds	the	bill	to	the	account	of	the	person	billed
with	the	lowest	balance,	and	marks	the	bill	as	unpaid. If	the	bill	is	not	paid,	
it	returns	an	error.
9. Create	a	procedure	Transfer, which	takes	three	parameters,	toAID,	
fromAID,	and	tAmount,	and transfers	the given	amount	between	the	two	
given	accounts	in	a	single	transaction. If	the	amount	is	not	available	in	the	
fromAID,	then	an	error	should	be	flagged	(hopefully	the	trigger	above	will	
take	care	of	this	for	you).
10. Create	a	procedure,	LoanMoney,	which	takes	three	parameters	AID,	
lAmount	and	lDueDate.	The	procedure	should	give	the	account	a	loan	of	
lAmount	and	also	create	a	bill	with	the	same	lAmount	and	due	date	on	
lDueDate
