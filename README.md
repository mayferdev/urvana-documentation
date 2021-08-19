# urvana-documentation
Urvana general documentation

# Postman  Documentation:
- Public Documentation: https://www.postman.com/mayferdev/workspace/urvana-public-workspace/collection/13659024-d3b33104-3b89-4027-a9f6-1d5d91285a41
- - When using this public documentaiton make sure to select the environment on the upper right corner -> appartmentEnvironment
- - - ![alt text](https://github.com/mayferdev/urvana-documentation/blob/main/assets/postman.jpg?raw=true)

- Postman collection and environment JSONs can be found under POSTMAN Directory (Useful for importing and then running on your own postman)

## how to use the api?
- Use the login method to log in and obtain a auth token as well as other firebase auth useful data. 
- The postman method already implements a tests which sets the auth token on the environment variable called: userToken which is already set up on all requests

# Entities and Description
### User
- A user can be a: 
- - Staff user (sign in using admin tool: https://appartment-admin.web.app/)
- - Staff users can be:
- - - Super admin
- - - Building (residential) manager
- - - Receptionist (security) 
- - owner: owns a property
- - tenant: lives and is the responsible for a property
- - sub_tenant: lives and is created by the tenant
- Users management use a mix of firebase and Urvana's DB. We use firebase to use the authentication, key management and password management. On the other side we use Urvana's own DB to store extra user information.

### Residential
- A residential is a group of properties for example: apartment building, condominium, residential.
- Residentials is a way to group properties, ammenities, rules, maintenance fees, administrative users, owners and tenants.

### Plan
- a plan is useful for knowing which plan the residential is registered to. 
- For example:
- - freemium, basic, pro, advanced
- this table allows us to know how much to charge the residential owner each month and which are the usage limits by feature or permissions by level. 

### Property
- A property is a single home or appartment
- A property has: an owner and a tenant.
- - properties are attached to users which at the end are the responsible for payments and management.
- - In some cases the owner and the tenant can be the same user.
- - In other cases the owner and the tenant will be different users.
- - In other cases a user can own multiple properties as well as be the main tenant (live in) multiple properties at the same time.  

### maintenance fees
- maintenance fees have a residential attached in order to be able to define whick fees apply to a specific residential
- - this is because fees might vary across residentials, For this purposes fees are specific to a residential, which we use to generate a monhtly balance to pay. 

### maintenance fee types
- a maintenance fee must have a type in order to know if it's a monhtly reccuring fee or a single charge fee
- if it's monhtly reccuring fee a cron will add it to the month's statement every x day of the month.
- - this correspondt to a recurring invoice generated every month
- If it's a single charge fee it must be manually added to a new monthly fee which equates to an individual, non-recurring invoice

### monhtly_fee
- a monhtly fee is actually the invoice generated monthy or the "monthly maintenance fee" which is generated every month and groups a set of maintenance fees that must be charged every month based on their type. 
- think of the monthly fee as the the invoice header whick includes:
- - property_id (who pays), total (total amount to pay), date (month to which it belongs), status (canceled 0, new (not paid) 1 or paid 2) 
- a monhtly fee groups maintenanfe fees using monthly_fee_detail table as pivot to join a many-many relation between each other.

### delivery
- a delivery is a way for receptionists to register food, correspondence, packages and others. for a property. 
- this is way to keep a log of how and when packages arrived with information about time delivered, who delivered, state of the package, and other metadata.
- this is mainly for security and administrative issues. 
- also when a delivery arrived users will receive a push notification telling them a package was delivered for their appartment.
- - when a delivery record is inserted, a push method (from back-end) must be executed to notify user *not done yet

### visit
- a visits is way for users to register visit from a visitor. 
- a visit contains date and time of arrival to inform the receptionist if a visitor is able to enter the residential with out the need to call or request for access. Think of a way of pre-approving visits 
- visit registers will also allow receptionist to register a visit altough if was not added by the user in the app. This will serve as security log.
- when a new visit is added a notification must be sent to the user as well. 

### visitor
- a visitor represents a person that is attached to a visit.
- we separated a visitor from a visit to be able to identify visitors from multiple visits.
- visitors have name, lastname and personal id information such as: front and back pictures from it's perosnal document, id number, and other metadata
- visitors could be marked as favourites in order to be able to be quickly added to a new visit record 

# Entities and Relationships Diagram
![alt text](https://github.com/mayferdev/urvana-documentation/blob/main/assets/diagram1.png?raw=true)


# Database Diagram
![alt text](https://github.com/mayferdev/urvana-documentation/blob/main/assets/DIAGRAM.png?raw=true)
