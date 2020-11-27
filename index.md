## Welcome to API Gateway for Tableta Inmultirii

[Swagger UI](dist)

[Swagger UI Preview](https://htmlpreview.github.io/?https://github.com/raducrs/tableta-inmultirii-api-gateway/blob/main/dist/index.html)

# tableta-inmultirii-api-gateway
API Gateway for Tableta Inmultirii

Contents 

- [Swagger UI live demo](https://raducrs.github.io/tableta-inmultirii-api-gateway/dist/index.html)
- [Swagger Definition](TabletaInmultirii-prod-swagger.json)
- [Swagger Definition + API Gateway Extensions](TabletaInmultirii-prod-swagger-apigateway.yaml)


## How to import Swagger Definition + API Gateway Extensions

Replace in `TabletaInmultirii-prod-swagger-apigateway.yaml` the definitions

- `arn:aws:apigateway:<region-apigateway>:lambda:path/2015-03-31/functions/arn:aws:lambda:<region-lambda>:<account-id>:function:`
   This are the lambda integration points
   
- `<ec2-hostname>:<port>` and `<Api-Key>` 
   This are the Spring backend integrations
   
- `<cognito-user-pool-authorizer-arn>` 
   This is the authorizer definitions
   
- `<S3-access-role>` and `<s3-public-bucket>`
   This is the S3 bucket integration
   
## Integration

All lambda integration points are defined in a separate repo

The Spring backend is defined in a separate repo

## Paths:
```
/auser/donations:
    POST:
        Lambda TI-AUser-DonationPost
  /{donationId}/code/{activationCode}:
    GET:
        Lambda TI-AUser-ConfirmationGet
/blackboard:
    GET:
        Lambda TI-UploadGetSignedUrl
/duser/{uid}/donations:
    GET:
        Lambda TI-DUser-GetDonations
    POST:
        Lambda TI-DUser-PostDonations
/feedback:
    POST:
        Lambda TI-SlackAlert
/puser/{pid}/donations
  /accepted:
    GET:
        Lambda TI-PUser-AcceptedGet
    POST:
        Lambda  TI-PUser-AcceptedPost
  /location:
    GET:
        Lambda TI-PUser-LocationGet
  /targeted:
    GET
        Lambda TI-PUser-TargetedGet
  /{donationId}:
    GET:
      Lambda TI-PUser-DetailsGet
    PUT:
      Lambda TI-PUser-StatusPut
    DELETE:
      Lambda TI-PUser-DonationDelete
/schools:
    GET:
	  Spring -> /schools/datapoints/history
  /datapoints/{json}:
    GET:
        S3 -> {bucket}/schools/datapoints/{object}
  /latest:
    GET:
       Spring -> /schools/datapoints/latest
/stats
  /gagdets:
    GET:
        Spring ->/stats/gadgets
  /{json}:
    GET:
        S3 -> /{bucket}/stats/{object}"
```
