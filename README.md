# The Official DocuSign C# Client

[![Nuget version][nuget-image]][nuget-url]
[![Nuget downloads][downloads-image]][downloads-url]
[![Build status][travis-image]][travis-url]

You can sign up for a free [developer sandbox](https://www.docusign.com/developer-center). 

Requirements
============

Microsoft .NET version 4.5 or later.

Installation
============

### NuGet Package Manager

To add to a new or existing Visual Studio project:  

	1. Open project and go to Tools -> NuGet Package Manager -> Manage NuGet Packages for Solution.
	2. Search for "DocuSign", select the DocuSign.eSign package, and click Install.  

### Manual Install 

Copy `DocuSign.eSign.dll` file to your local machine and add reference through your project settings.

### Others

Alternatively you can just copy the source code directly into your project. 

#### Dependencies

This client has the following external dependencies: 

* Newtonsoft.Json.dll
* RestSharp.dll
* BouncyCastle
* System.IdentityModel.Tokens.Jwt

Usage
=====

To send a signature request from a template using OAuth JWT authentication:

```csharp
using DocuSign.eSign.Api;
using DocuSign.eSign.Model;
using DocuSign.eSign.Client;
using System.Collections.Generic;
using DocuSign.eSign.Client.Auth;

namespace DocuSignSample
{
	class Program
	{
		static void Main(string[] args)
		{
			string userId = "[USER_ID]"; // use your userId (guid), not email address
			string oauthBasePath = "[OAUTH_BASE_PATH]";
			string integratorKey = "[INTEGRATOR_KEY]";
			string privateKeyFilename = "[PRIVATE_KEY_FILENAME]";
			int expiresInHours = 1;
			string host = "https://demo.docusign.net/restapi";

			string accountId = string.Empty;

			ApiClient apiClient = new ApiClient(host);
			OAuth.OauthToken tokenInfo = apiClient.ConfigureJwtAuthorizationFlowByKey(integratorKey, userId, oauthBasePath, privateKey, expiresInHours);

			/////////////////////////////////////////////////////////////////
			// STEP 1: Get User Info   
			// now that the API client has an OAuth token, let's use it in all// DocuSign APIs
			/////////////////////////////////////////////////////////////////
			
			OAuth.UserInfo userInfo = testConfig.ApiClient.GetUserInfo(tokenInfo.access_token);

			string accountId = string.Empty;

			foreach (var item in userInfo.GetAccounts())
			{
				if(item.GetIsDefault() == "true")
				{
					accountId = item.AccountId();
					apiClient = new ApiClient(item.GetBaseUri() + "/restapi");
					break;
				}
			}

			/////////////////////////////////////////////////////////////////
			// STEP 2: CREATE ENVELOPE API        
			/////////////////////////////////////////////////////////////////				

			EnvelopeDefinition envDef = new EnvelopeDefinition();
			envDef.EmailSubject = "[DocuSign C# SDK] - Please sign this doc";

			// assign recipient to template role by setting name, email, and role name.  Note that the
			// template role name must match the placeholder role name saved in your account template.  
			TemplateRole tRole = new TemplateRole();
			tRole.Email = "[SIGNER_EMAIL]";
			tRole.Name = "[SIGNER_NAME]";
			tRole.RoleName = "[ROLE_NAME]";
			List<TemplateRole> rolesList = new List<TemplateRole>() { tRole };

			// add the role to the envelope and assign valid templateId from your account
			envDef.TemplateRoles = rolesList;
			envDef.TemplateId = "[TEMPLATE_ID]";

			// set envelope status to "sent" to immediately send the signature request
			envDef.Status = "sent";

			// |EnvelopesApi| contains methods related to creating and sending Envelopes (aka signature requests)
			EnvelopesApi envelopesApi = new EnvelopesApi(apiClient.Configuration);
			EnvelopeSummary envelopeSummary = envelopesApi.CreateEnvelope(accountId, envDef);
		}
	}
}
```

See [CoreRecipes.cs](https://github.com/docusign/docusign-csharp-client/blob/master/test/Recipes/CoreRecipes.cs) for more examples.

# Authentication

## Service Integrations that use Legacy Header Authentication

([Legacy Header Authentication](https://docs.docusign.com/esign/guide/authentication/legacy_auth.html) uses the X-DocuSign-Authentication header.)

1. Use the [Authentication: login method](https://docs.docusign.com/esign/restapi/Authentication/Authentication/login/) to retrieve the account number **and the baseUrl** for the account.
The url for the login method is www.docusign.net for production and demo.docusign.net for the developer sandbox.
The `baseUrl` field is part of the `loginAccount` object. See the [docs and the loginAccount object](https://docs.docusign.com/esign/restapi/Authentication/Authentication/login/#/definitions/loginAccount)
2. The baseUrl for the selected account, in production, will start with na1, na2, na3, eu1, or something else. Use the baseUrl that is returned to create the *basePath* (see the next step.) Use the basePath for all of your subsequent API calls.
3. As returned by login method, the baseUrl includes the API version and account id. Split the string to obtain the *basePath*, just the server name and api name. Eg, you will receive `https://na1.docusign.net/restapi/v2/accounts/123123123`. You want just `https://na1.docusign.net/restapi` 
4. Instantiate the SDK using the basePath. Eg `ApiClient apiClient = new ApiClient(basePath);`
5. Set the authentication header as shown in the examples by using `Configuration.Default.AddDefaultHeader`

## User Applications that use OAuth Authentication
1. After obtaining a Bearer token, call the [OAuth: Userinfo method](https://docs.docusign.com/esign/guide/authentication/userinfo.html). Obtain the selected account's `base_uri` (server name) field.
The url for the Userinfo method is account-d.docusign.com for the demo/developer environment, and account.docusign.com for the production environment.
1. Combine the base_uri with "/restapi" to create the basePath. The base_uri will start with na1, na2, na3, eu1, or something else. Use the basePath for your subsequent API calls.
4. Instantiate the SDK using the basePath. Eg `ApiClient apiClient = new ApiClient(basePath);`
5. Create the `authentication_value` by combining the `token_type` and `access_token` fields you receive from either an [Authorization Code Grant](https://docs.docusign.com/esign/guide/authentication/oa2_auth_code.html) or [Implicit Grant](https://docs.docusign.com/esign/guide/authentication/oa2_implicit.html) OAuth flow. 
5. Set the authentication header by using `Configuration.Default.AddDefaultHeader('Authorization', authentication_value)`


Testing
=======

Unit tests are available in the [Test](/test/SdkTests) folder. 

Support
=======

Feel free to log issues against this client through GitHub.  We also have an active developer community on Stack Overflow, search the [DocuSignAPI](http://stackoverflow.com/questions/tagged/docusignapi) tag.

License
=======

The DocuSign CSharp Client is licensed under the following [License](LICENSE).


[nuget-image]: https://img.shields.io/nuget/v/DocuSign.eSign.dll.svg?style=flat
[nuget-url]: https://www.nuget.org/packages/DocuSign.eSign.dll
[downloads-image]: https://img.shields.io/nuget/dt/DocuSign.eSign.dll.svg?style=flat
[downloads-url]: https://www.nuget.org/packages/DocuSign.eSign.dll
[travis-image]: https://img.shields.io/travis/docusign/docusign-csharp-client.svg?style=flat
[travis-url]: https://travis-ci.org/docusign/docusign-csharp-client
