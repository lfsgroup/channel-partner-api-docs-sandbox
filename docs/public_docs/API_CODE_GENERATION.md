# Generating Code from the API spec

Client Code may be generated to interact with FeeWise from the [openapi-spec](https://swagger.io/specification/). Using 
generated code means the boilerplate of making the HTTP requests is done for you and FeeWise appears as a library in your 
chosen language.

The FeeWise partner API spec can be downloaded.  

```shell
curl https://stoplight.io/api/v1/projects/feewise/channel-partner-api-docs/nodes/reference/partner-openapispec.yaml
```

[Stoplight](https://feewise.stoplight.io/docs/channel-partner-api-docs/4a91a3bcef6bd-fee-wise-partner-api) also has an Export' button 

There are many code generators available.   
One of the most supported is [openapi-generator](https://github.com/OpenAPITools/openapi-generator), which generates 
client code for many languages. 


## C# client on nuget

FeeWise automatically generates and publishes a C# library to access the FeeWise API. This is published to nuget

See [FeeWise on nuget](https://www.nuget.org/packages/FeeWise#readme-body-tab) for usage.