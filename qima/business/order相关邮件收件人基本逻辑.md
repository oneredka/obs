

set To 
if sub and isMasterAccountWantReceiveEmail
	add master's all email 
else 	
	if sendNotificationMailType == who booked the order
		add user‘s  current personal email
	if 	sendNotificationMailType == alternative Contact
	   add  user’s all email
   if sendNotificationMailType == both
      add user‘s  current personal email 
      add  user’s all email
	   
set Cc
if sub and isMasterAccountWantReceiveEmail and  isMasterAccountCcToSupplier

	if sendNotificationMailType == who booked the order
		add user‘s  current personal email
	if 	sendNotificationMailType == alternative Contact
	   add  user’s all email
    if sendNotificationMailType == both
      add user‘s  current personal email 
      add  user’s all email


set BCC 
if sub and isMasterAccountWantReceiveEmail and isMasterAccountBccToSupplier
	if sendNotificationMailType == who booked the order
		add user‘s  current personal email
	if 	sendNotificationMailType == alternative Contact
	   add  user’s all email
    if sendNotificationMailType == both
      add user‘s  current personal email 
      add  user’s all email

always

BCC  ` chinainspection@gmail.com` 

if order.getCopyAllMailTo() is not null 
	add order.getCopyAllMailTo() to cc







