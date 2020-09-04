+++
title = "Using Auth.AuthToken for API integrations"
date = "2020-08-14T00:41:51-04:00"
author = "Bergin Panimayam"
excerpt = "How to use Auth.AuthToken to securely and optimally for Salesforce API integrations."
type = "post"
slug = "using-auth-authtoken-for-api-integrations"
image = "/images/post/pexels-pixabay-60504-1-825x510.jpg" 
categories = ["API"]
tags = ["Access token","API","Integration","OAuth2","Refresh token","Salesforce","Token"]
+++
When it comes to API integration with systems that have sensitive data, security is something you could never compromise. Yet, you need to find a balance on how you design a solution that is secure and optimal as it should be, so it doesn&#8217;t choke on scaling.

### **Requirement** {.has-medium-font-size}

You have a Single Sign-on AuthProvider setup using OpenID Connect for the users to log in to Salesforce. You need to pass the user&#8217;s access token in the API call, so the service can authenticate the user before executing the API request. Also, the access token provided by the AuthProvider is valid only for 15 minutes for security reasons and the refresh token is valid for 12 hours.

### **Using AccessToken to validate user** {.has-medium-font-size}

In a typical solution, you might get the access token and add it to your HttpRequest and make the API call. The server might check the validity of the token to make sure the user is in session and an authorized user.

However, since the access token is valid for only 15 minutes, you need to make sure the token you add to your HttpRequest is valid and avoid a 401 unauthorized response. Let&#8217;s see how you can handle this.

### **Auth.AuthToken class** {.has-medium-font-size}

Salesforce provides the [Auth.AuthToken class](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_class_Auth_AuthToken.htm#apex_class_Auth_AuthToken) to retrieve and revoke the access token. Let's focus on using two methods that can be used in this use case.

``` apex
getAccessToken(authProviderId, providerName)
refreshAccessToken(authProviderId, providerName, oldAccessToken)
```

When you call the getAccessToken() method, for the first time, Salesforce makes a call to your AuthProvider to get the access token and holds in the cache &#8212; meaning Salesforce doesn&#8217;t go to the AuthProvider each time for getAccessToken() call, you get the same token until it&#8217;s refreshed.

So, how to make sure you pass a valid token in the API request every time, without making a call to the AuthProvider to introspect if the token is valid or not? The easiest way is to make a refreshAccessToken() call to get a &#8220;refreshed&#8221; accessToken and use it to make the API request. But it might be expensive too, to make a refreshAccessToken() call every time you need to make an API call &#8212; this would be an issue if the number of calls you make in a given time is too high. Another option is to handle 401 unauthorized error and retry the API call with a refreshed access token &#8211; which could be tedious and result in unnecessary calls that could count towards your API limit.

### **Solution &#8212; Validating the access token locally** {.has-medium-font-size}

<p class="has-medium-font-size">
  You can decode the access token to get the contents of the token. The access token has a property called &#8220;exp&#8221; &#8212; expiration time of the token.
</p>

```
{ 
  ... 
  "iat": 1597374960, 
  "exp": 1597378240, 
  ... 
}
```

Check the exp against the current time, if the token is expired, make a refreshAccessToken() call to get a new access token. To be on the safer side, I&#8217;d add a buffer to the current time &#8212; say 60 seconds &#8212; and compare against the exp time, if it&#8217;s still within the current time ( minus 1 minute), then use the same token, else, get a new refreshed token.

This way you can avoid,

  * Making unnecessary calls to refreshAccessToken()
  * 401 unauthorized errors from the service provider for an invalid token and retry API calls with a valid tokens
  * Introspection calls to the auth provider to validate the access token&#8217;s validity.


This helps in reducing the number of unnecessary API calls you make to the service provider and the AuthProvider and avoid API limit issues while making secure API calls.

[Click here to read this article on Medium.](https://medium.com/bergin-io/using-auth-authtoken-for-api-integrations-a9963982e34e)
