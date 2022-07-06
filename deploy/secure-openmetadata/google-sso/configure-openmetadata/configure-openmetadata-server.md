# Configure OpenMetadata Server

## Update conf/openmetadata.yaml

Once the `client id` and `client secret` are generated, add `client id` as the value of the `clientId` field in the openmetadata.yaml file. See the snippet below for an example of where to place the `client id` value.

```
authenticationConfiguration:
  provider: "google"
  publicKeyUrls: 
    - "https://www.googleapis.com/oauth2/v3/certs"
  authority: "https://accounts.google.com"
  clientId: "{client id}"
  callbackUrl: "http://localhost:8585/callback"
```

Then, 
- Update `authorizerConfiguration` to add login names of the admin users in `adminPrincipals` section as shown below.
- Update the `principalDomain` to your company domain name. 

```
authorizerConfiguration:
  className: "org.openmetadata.catalog.security.DefaultAuthorizer"
  # JWT Filter
  containerRequestFilter: "org.openmetadata.catalog.security.JwtFilter"
  adminPrincipals:
    - "user1"
    - "user2"
  botPrincipals:
    - "ingestion-bot"
  principalDomain: "open-metadata.org"
```