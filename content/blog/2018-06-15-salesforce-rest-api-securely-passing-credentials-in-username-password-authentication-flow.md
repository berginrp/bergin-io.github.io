---
id: 179
title: 'Salesforce Rest API &#8211; Securely passing credentials in Username-password authentication flow'
date: 2018-06-15T14:41:58-04:00
author: Bergin Panimayam
layout: post
guid: http://www.bergin.in/?p=179
permalink: /2018/06/15/salesforce-rest-api-securely-passing-credentials-in-username-password-authentication-flow/
avada_post_views_count:
  - "0"
categories:
  - API
tags:
  - Authentication Flow
  - REST API
  - Username-Password
---
When an external system makes a call to a Salesforce Rest API, to get the auth token, you call the oauth2/token api with username-password authentication flow takes the credentials in plain text. This raises security concerns.

<a href="https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_username_password_oauth_flow.htm" target="_blank" rel="noopener"><img loading="lazy" class="aligncenter" title="https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_username_password_oauth_flow.htm" src="https://developer.salesforce.com/docs/resources/img/en-us/214.0?doc_id=dev_guides%2Fapi_rest%2Fimages%2Foauth_username_password_flow.png&folder=api_rest" alt="Username-password OAuth authentication flow" width="493" height="537" /></a>

Looks like there&#8217;s no alternative other than passing username & password and clientId & secrete as plain text in the username-password authentication flow.

<pre>grant_type=password&client_id=3MVG9lKcPoNINVBIPJjdw1J9LLM82Hn
FVVX19KY1uA5mu0QqEWhqKpoW3svG3XHrXDiCQjK1mdgAvhCscA9GE&client_secret=
1955279925675241571&username=testuser%40salesforce.com&password=mypassword123456</pre>

> I&#8217;ve raised an idea to enable a way to securely send the clientId & secret and the username & password. Please vote for this idea at <a href="https://success.salesforce.com/ideaView?id=0873A000000EA5yQAG" target="_blank" rel="noopener">https://success.salesforce.com/ideaView?id=0873A000000EA5yQAG.</a>

If you have other solutions for this, please share it here.