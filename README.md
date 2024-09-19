# Transportation_Service
The registered employees of any company portal will be able to avail the transportation services. This module will provide the following services to the employees. 
1.	Search for the available transportation services 
2.	Subscribe to the transportation service 
3.	Unsubscribe from a transportation service. 

Note: Pre-populate few records in the Transporation services tables 


Stage 1 : Database Implementation 

1.	Design a data base as per the following ER diagram provided. 
2.	Enfore the following additional constraints apart from primary key, foreign key and unique keys 
a.	Return time must also be greater than start time 
b.	Driver phone must be exactly 10 digits 
c.	Current capacity should not exceed maximum capacity 
d.	Payment date should be automatically taken 
e.	Subscription end date should not be less then subscription start date 
f.	Allowed values for subscription status are – Active, Expired, Cancelled

Stage 2 : Data Access Layer Design

1.	Created a library project and add ORM support into it.  
2.	Used the ORM to map the entities to database as per the ER diagram provided.  
3.	Used repository per entity pattern and generate the repositories to perform the following operations 
a.	Return the available transports based on pickup point 
b.	Add a new subscription 
c.	Update an existing subscription 
d.	Fetch fare for a transportation service 
e.	Update the transportation capacity 
 
Stage 3 : Business Logic Layer Development 
 
1.	Developed a library which reference the Data Access Library project created earlier 
2.	This class library will contain various service classes which will encapsulate the business logic for the application. 
3.	Use dependency injection to in service classes to inject the required repositories. 
4.	Created the service classes following the single responsibility principle which perform the given operations as follows  
a.	Fetch available transportation for a given pickup point 
b.	Create a new subscription and pay for it 
c.	Cancel a subscription and return refundable amount 
d.	View a subscription by id 
e.	Calculate the total fare for a given subscription 
f.	Update the current capacity 
5.	Following business rules must be implemented as part of the business service class 
a.	When user searches for transportation display only those which are available for booking 
b.	Employees can subscribe to monthly, quarterly, half yearly and yearly services. Subscription end date must be accordingly generate and amount payable must be displayed accordingly. 
c.	Whenever a user successfully subscribes/unsubscribes to a service then the current capacity must be updated accordingly 
d.	Whenever a subscription is successfully created an auto-generated subscriptionid must be displayed backed 
 
Stage 4 : Unit Testing 

1.	Created a new Unit test project to test the service classes created in business logic layers 
2.	Mock all the repositories using a mocking framework. 
 
Stage 5 : Micro-service implementation 

1.	Created an API project which references the business logic layer created earlier 
2.	Implement service documentation using swagger 
3.	Created the following end-points and test them using postman and export the requests into a json file.
   
Table 1 : Transportation Service - Endpoint - 1 
URL 	api/transports/<pickup-point> 
Request Type 	GET 
User Role 	All registered users 
Trigger 	Front end 
Description 	Users should be able to view the available transporation services for their pickup locations 
Inputs 	Pickup point 
Outputs 	TransportationServicesDTOs 

Table 2 : Transportation Service - Endpoint - 2 
URL 	api/subscriptions/new 
Request Type 	POST 
User Role 	All registered users 
Trigger 	Front end 
Description 	If a transportation is available user should be able to subscribe to it by making a payment 
Inputs 	SubscribeDTO with subscription details and payment details 
Outputs 	Status code or error messages 

Table 3 : Transportation Service - Endpoint - 3 
URL 	api/transports/calculatefare 
Request Type 	POST 
User Role 	All registered users 
Trigger 	Front end 
Description 	User will be able to view the applicable fare for the plan they have selected 
Inputs 	FareDTO  
Outputs 	Fare amount and status code 

Table 4 : Transportation Service - Endpoint - 4 
URL 	api/subscription/<subscription-id> 
Request Type 	GET 
User Role 	All registered users 
Trigger 	Front end 
Description 	A user having a subscription should be able to view the subscription details 
Inputs 	Subscription id 
Outputs 	SubscriptionDetailsDTO including subscription details and selected transportation details 

Table 5 : Transportation Service - Endpoint - 5 
URL 	api/subscriptions/<subscriptionid>/unsubscribe 
Request Type 	DELETE 
User Role 	All registered users 
Trigger 	Front end 
Description 	A subscribed user with an active subscription must be able to cancel the subscription 
Inputs 	Subscriptionid 
Outputs 	Status code  
 
Stage 6 : Front end design 
 
1.	Created the following components as per the specification provided below.  
a.	SearchTransportationComponent 
1.	Create a component which allows users to view the currently available transportation services in a tabular format 
2.	User should provide a pickup location and click the search button to view the available transport services 
3.	If a service is available it should have a button to subscribe 
4.	Provide a navigation link in the navbar of the application to access the component 
 
b.	SubscribeTransportationComponent 
1.	Create a component which will show the transporation detail to the user for a particular transportation selected by user in search transporation component. 
2.	It should display all the transportation details and accept the subscription details and payment options 
3.	Subscription duration should be selected from a set of radio button and payment mode must be selected via a drop down list 
4.	Once a user selects these details calculate and display the fare to the user 
5.	Once all the details are validated then user should be able to subcribe by clicking the subscribe button. 
 
c.	CancelSubscriptionComponent 
1.	A logged in user should be able to navigate to cancel subscription component 
2.	Create a cancel subscription component which will accept the subscription id and displays the subscription details to the user 
3.	If the current status of subscription is active user should be able to cancel 
 
Stage 7 : Integration of Frontend and backend 
1.	Create a data service in the Front end application which will communicate with the Micro services. 
2.	Use the data service in the components to make them interact with the API 
3.	Valid error messages should be shown based on various response status codes received form the API .

