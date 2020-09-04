---
id: 217
title: 'Salesforce Rest API &#8211; Create Case'
date: 2018-11-06T13:43:01-05:00
author: Bergin Panimayam
layout: post
guid: http://www.bergin.in/?p=217
permalink: /2018/11/06/salesforce-rest-api-create-case/
fusion_builder_status:
  - 'off'
avada_post_views_count:
  - "0"
image: /wp-content/uploads/2018/11/featured_pic_rest_api-825x510.png
categories:
  - API
tags:
  - Case
  - Insert
  - REST API
---
Salesforce provides standard APIs for many of the actions one would need to perform.





  * Request information about the version of the API
  * Get detail information about a Salesforce object like Account, Case or Custom Object
  * Perform CRUD operation on a Salesforce standard or custom object





This makes it easier to integrate with Salesforce with these standard APIs. Let&#8217;s see how to create a case using the Rest API.





  1. Get access token &#8211; here we&#8217;ll use the username-password flow to get the OAuth <pre class="wp-block-code berg-code"><code>Bearer &lt;access_token&gt;</code></pre>
    
  
    <pre class="wp-block-code berg-code"><code>POST /services/oauth2/token HTTP/1.1 
Host: login.salesforce.com X-PrettyPrint: 1 
Content-Type: application/x-www-form-urlencoded 
grant_type=password&amp; 
client_id=3MVG9lKcPoNINVBIPJjdw1J9LLM82HnFVVX19KY1uA5mu0QqEWhqKpoW3svG3XHrXDiCQjK1mdgAvhCscA9GE&amp; 
client_secret=1955279925675241571&amp;
username=testuser%40salesforce.com&amp; 
password=mypassword123456fgshjdfsdljfhsdhfsdfs</code></pre> token using Client ID & Secret.

  2. The next step is to use the access token and the instance_url from the response from Step 1 <pre class="wp-block-code berg-code"><code>{
  "access_token":"XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "instance_url": "https://yourdomain.my.salesforce.com",
  "id":"https://login.salesforce.com/id/XXXXXXXXXXXXXXXXXX/XXXXXXXXXXXXXXXXXX",
  "token_type": "Bearer",
  "issued_at": "1454735969118",
  "signature": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX="
}</code></pre> and make the actual RestAPI call to create the case.





### **Get Access Token &#8211; Request**





Set up a connected app in Salesforce and get the Client ID and Secret. Create an API only user and get the username, password, and security token.





Note: the password in the request includes password & security-token combined.





<pre class="wp-block-code berg-code"><code>POST /services/oauth2/token HTTP/1.1 
Host: login.salesforce.com X-PrettyPrint: 1 
Content-Type: application/x-www-form-urlencoded 
grant_type=password&amp; 
client_id=3MVG9lKcPoNINVBIPJjdw1J9LLM82HnFVVX19KY1uA5mu0QqEWhqKpoW3svG3XHrXDiCQjK1mdgAvhCscA9GE&amp; 
client_secret=1955279925675241571&amp;
username=testuser%40salesforce.com&amp; 
password=mypassword123456fgshjdfsdljfhsdhfsdfs</code></pre>



### Response



<pre class="wp-block-code berg-code"><code>{
  "access_token":"XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "instance_url": "https://yourdomain.my.salesforce.com",
  "id":"https://login.salesforce.com/id/XXXXXXXXXXXXXXXXXX/XXXXXXXXXXXXXXXXXX",
  "token_type": "Bearer",
  "issued_at": "1454735969118",
  "signature": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX="
}</code></pre>





### ****Call the create Case RestAPI with access_token from the previous step****





Use the instance\_url and the access\_token from the previous step to make the call to create a Case.





Use access_token in Authorization Header as Authorization:





<pre class="wp-block-code berg-code"><code>Bearer &lt;access_token&gt;</code></pre>





Use the <instance_url> along with the endpoint to access the intended API.





Create Case RestAPI request





<pre class="wp-block-code berg-code"><code>POST services/data/v42.0/sobjects/Case 
Host: &lt;instance_url&gt;
Authorization: Bearer &lt;access_token&gt;

Content-Type: application/json
{
   "Subject": "subject goes here",
   ...
   ...
}</code></pre>





### **Response**





<pre class="wp-block-code berg-code"><code>201 Created

{
    "id": "a002800000PA0AzAAL",
    "success": true,
    "errors": []
}</code></pre>





That&#8217;s it, you&#8217;ve created a case using RestAPI!





Here&#8217;s are some **useful links,**





**REST API:**  
<a href="https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_what_is_rest_api.htm" target="_blank" rel="noreferrer noopener">https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_what_is_rest_api.htm</a>





**Authentication:**  
<a href="https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm" target="_blank" rel="noreferrer noopener">https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm</a>





**Create Record Example:  
** (For creating case, replace “Account” with “Case”), use appropriate request body.)  
<a href="https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm" target="_blank" rel="noreferrer noopener">https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm</a>





**Case Object & Fields:**  
<a href="https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_case.htm" target="_blank" rel="noreferrer noopener">https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_case.htm</a>