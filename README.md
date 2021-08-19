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

### Property
- A property is a single home or appartment
- A property has: an owner and a tenant.
- - In some cases the owner and the tenant can be the same user.
- - In other cases the owner and the tenant will be different users.
- - In other cases a user can own multiple properties as well as be the main tenant (live in) multiple properties at the same time.  

# Entities and Relationships Diagram

# Database Diagram
![alt text](https://github.com/mayferdev/urvana-documentation/blob/main/assets/DIAGRAM.png?raw=true)
