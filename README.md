# AWS Lambda Authorizer for Okta API Authorzation Server

This Lambda Authorizer integrates with Okta' API Access Management to secure endpoints proxied by the AWS API Gateway.  In this architecture, the AWS API Gateway acts as the PEP where as Okta acts as the PDP and PIP.  The highlevel flow includes:

1. Client obtains an access token from Okta per standard flow but does not need to request specfic access scopes (except standard ones i.e openid profile)
2. Client invokes API proxied by AWS API Gateway 
3. Authorizer validates Okta token and requests API AM policies that are relevant for this client
4. Authorizer checks if there is a matching scope for this method and resource being invoke.  Scope names are in the format of "METHOD/RESOURCE"
5. If a scope exists than the request is sent through

The values of this authorizer include

- Clients do not need to request specific scopes or understand the possible scopes that exist
- All authentications and minting of tokens are centralized
- All authorizations and policies are centralized
- Changes to security policies are processed scopes have ZERO impact to clients, APIs, and API GW configuations 

