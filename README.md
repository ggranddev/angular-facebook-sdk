[![npm](https://img.shields.io/npm/l/express.svg)](https://www.npmjs.com/package/ng2-facebook-sdk)

[![NPM](https://nodei.co/npm/ng2-facebook-sdk.png?stars&downloads)](https://nodei.co/npm/ng2-facebook-sdk/)


# Angular2 Facebook SDK
This is a wrapper for the official Facebook JavaScript SDK. You must still include their JavaScript files in your project. This wrapper makes it easier to use Facebook SDK with Angular2 by providing types and promises.

- [Installation](#installation)
- [Example Usage](#example-usage)
- [Methods](#methods)
    - [init](#init)
    - [api](#api)
    - [ui](#ui)
    - [getLoginStatus](#getloginstatus)
    - [login](#login)
    - [logout](#logout)
    - [getAuthResponse](#getauthresponse)
- [Interfaces](#interfaces)
    - [FacebookInitParams](#facebookinitparams)
    - [FacebookApiMethod (enum)](#facebookapimethod)
    - [ShareDialogParams](#sharedialogparams)
    - [ShareDialogResponse](#sharedialogresponse)
    - [FeedDialogParams](#feeddialogparams)
    - [FeedDialogResponse](#feeddialogresponse)
    - [SendDialogParams](#senddialogparams)
    - [FacebookUiParams](#facebookuiparams)
    - [FacebookUiResponse](#facebookuiresponse)
    - [FacebookAuthResponse](#facebookauthresponse)
    - [FacebookLoginStatus](#facebookloginstatus)
    - [FacebookLoginOptions](#facebookloginoptions)
    - [FacebookLoginResponse](#facebookloginresponse)


## Installation
- Install via NPM:
```
npm i --save-dev ng2-facebook-sdk
```

- Add the Facebook JavaScript SDK to your index.html
```
<script type="text/javascript" src="https://connect.facebook.net/en_US/sdk.js"></script>
```


## Example Usage
```typescript
import {FacebookService, FacebookLoginResponse} from 'ng2-facebook-sdk';

@Component({
  templateUrl: '/path/to/template.html',
  providers: [FacebookService]
})
export class MyComponent {
  constructor(private fb: FacebookService) { }

  someFunction(): void {
    this.fb.login().then(
      (response: FacebookLoginResponse) => console.log(response),
      (error: any) => console.error(error)
    );
  }
}
```


# Methods

## init

This method is used to initialize and setup the SDK.

**Parameters**

-   `params` { [FacebookInitParams](#facebookinitparams)} Options to initialize the app with

#### Example
```typescript
import {FacebookService, FacebookInitParams} from 'ng2-facebook-sdk';

@Component(...)
export class MyComponent {
  constructor(private fb: FacebookService) {
    let fbParams: FacebookInitParams = {
                                   appId: '1234566778',
                                   xfbml: true,
                                   version: 'v2.6'
                                   };
    this.fb.init(fbParams);
  }
}
```


## api
This method lets you make calls to the Graph API

**Parameters**

-   `path`  This is the Graph API endpoint path that you want to call.
-   `method`  This is the HTTP method that you want to use for the API request.
-   `params`  This is an object consisting of any parameters that you want to pass into your Graph API call.

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;any>**

## ui

This method is used to trigger different forms of Facebook created UI dialogs.
These dialogs include:

-   Share dialog
-   Login dialog
-   Add page tab dialog
-   Requests dialog
-   Send dialog
-   Payments dialog
-   Go Live dialog

**Parameters**

-   `params`  A collection of parameters that control which dialog is loaded, and relevant settings.

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;FacebookUiResponse>**

## getLoginStatus

This method allows you to determine if a user is logged in to Facebook and has authenticated your app.

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;FacebookLoginStatus>**

## login

Login the user

**Parameters**
-   `options`

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;FacebookLoginResponse>**

## logout

Logout the user

Returns **[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)&lt;any>**

## getAuthResponse

This synchronous function returns back the current authResponse.

Returns **FacebookAuthResponse**



# Interfaces


## FacebookInitParams
Name    |   Type    |   Description
:--- |:--- |:--- 
appId   | `string`  |   Your application ID. If you don't have one find it in the App dashboard or go there to create a new app. **Defaults to `null`**.
version   | `string`  |   Determines which versions of the Graph API and any API dialogs or plugins are invoked when using the `.api()` and `.ui()` functions. Valid values are determined by currently available versions, such as 'v2.0'. **This is a required parameter**.
cookie   | `boolean`  |   Determines whether a cookie is created for the session or not. If enabled, it can be accessed by server-side code. **Defaults to `false`**.
status   | `boolean`  |   Determines whether the current login status of the user is freshly retrieved on every page load. If this is disabled, that status will have to be manually retrieved using `.getLoginStatus()`. **Defaults to `false`**.
xfbml   | `boolean`  |   Determines whether XFBML tags used by social plugins are parsed, and therefore whether the plugins are rendered or not. **Defaults to `false`**.
frictionlessRequests   | `boolean`  |   Frictionless Requests are available to games on Facebook.com or on mobile web using the JavaScript SDK. This parameter determines whether they are enabled. **Defaults to `false`**.
hideFlashCallback   | `function`  |   This specifies a function that is called whenever it is necessary to hide Adobe Flash objects on a page. This is used when `.api()` requests are made, as Flash objects will always have a higher `z-index` than any other DOM element. See our Custom Flash Hide Callback for more details on what to put in this function. **Defaults to `null`**.

## FacebookApiMethod
Name    |   Description
:--- |:--- 
get |   Get request
post | Post request
delete | Delete request

## ShareDialogParams
Name    |   Type    |   Description
:--- | :--- | :---
href | `string` | The link attached to this post. Required when using method share. Include open graph meta tags in the page at this URL to customize the story that is shared. Defaults to the current URL.
hashtag | `string` | A hashtag specified by the developer to be added to the shared content. People will still have the opportunity to remove this hashtag in the dialog. The hashtag should include the hash symbol, e.g. #facebook.
quote | `string` | A quote to be shared along with the link, either highlighted by the user or predefined by the developer, as in a pull quote on an article.
mobile_iframe | `string` | If set to true the share button will open the share dialog in an iframe on top of your website (For more information see Mobile Web Share Dialog. This option is only available for mobile, not desktop.
action_type | `string` | A string specifying which Open Graph action type to publish, e.g., og.likes for the built in like type. The dialog also supports approved custom types. Required when using method share_open_graph.
action_properties_type | `string` | A JSON object of key/value pairs specifying parameters which correspond to the action_type being used. Valid key/value pairs are the same parameters that can be used when publishing Open Graph Actions using the API. Required when using method share_open_graph.

## ShareDialogResponse
Name    |   Type    |   Description
:--- | :--- | :---
post_id | `string` | Only available if the user is logged into your app using Facebook and has granted publish_actions. If present, this is the ID of the published Open Graph story.
error_message | `string` | Only available if the user is logged into your app using Facebook Login.

## FeedDialogParams 
Name    |   Type    |   Description
:--- | :--- | :---
from | `string` | The ID of the person posting the message. If this is unspecified, it defaults to the current person. If specified, it must be the ID of the person or of a page that the person administers.
to | `string` | The ID of the profile that this story will be published to. If this is unspecified, it defaults to the value of from. The ID must be a friend who also uses your app.
link | `string` | The link attached to this post. With the Feed Dialog, people can also share plain text status updates with no content from your app; just leave the link parameter empty.
picture | `string` | The URL of a picture attached to this post. The picture must be at least 200px by 200px. See our documentation on sharing best practices for more information on sizes
source | `string` | The URL of a media file (either SWF or MP3) attached to this post. If SWF, you must also specify picture to provide a thumbnail for the video.
name | `string` | The name of the link attachment.
caption | `string` | The caption of the link (appears beneath the link name). If not specified, this field is automatically populated with the URL of the link.
description | `string` | The description of the link (appears beneath the link caption). If not specified, this field is automatically populated by information scraped from the link, typically the title of the page.
ref | `string` | This argument is a comma-separated list, consisting of at most 5 distinct items, each of length at least 1 and at most 15 characters drawn from the set '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz_'. Each category is used in Facebook Insights to help you measure the performance of different types of post

## FeedDialogResponse
Name    |   Type    |   Description
:--- | :--- | :---
post_id | `string` | The ID of the posted story, if the person chose to publish to their timeline.

## SendDialogParams
Name    |   Type    |   Description
:--- | :--- | :---
to  | `string` | A user ID of a recipient. Once the dialog comes up, the sender can specify additional people as recipients.
link    | `string` | Required parameter. The URL that is being sent in the message.

## FacebookUiParams
This interface extends [ShareDialogParams](#sharedialogparams), [FeedDialogParams](#feeddialogparams) and [SendDialogParams](#senddialogparams). It also contains the following properties:

Name    |   Type    |   Description
:--- | :--- | :---
method  |   `any` |   The UI dialog that is being invoked. **This is a required field.**
app_id  |   `string`    |   Your app's unique identifier. **Required.**
redirect_uri    | `string`  | The URL to redirect to after a person clicks a button on the dialog. **Required when using URL redirection.**
display |   `string`    | Determines how the dialog is rendered.
phase   |   `string`    |   Dialog in create phase allows you to get stream url to upload video; Dialog in publish phase will provide preview and go live button. **Required**. Value can be `create` or `publish`.
broadcast_data  |   `any`   |   The response object returned from either API or create phase. **This parameter is required for publish phase.**

## FacebookUiResponse
This interface extends [ShareDialogResponse](#sharedialogresponse) and [FeedDialogResponse](#feeddialogresponse).

## FacebookAuthResponse
Name    |   Type    |   Description
:--- |:--- |:--- 
accessToken|`string`|User access token
expiresIn|`number`|Access token lifetime in seconds
signedRequest|`string`|
userID|`string`|The Facebook user ID

## FacebookLoginStatus
Name    |   Type    |   Description
:--- |:--- |:--- 
status|`string`|Status
authResponse|`FacebookAuthResponse`| Facebook AuthResponse object

###FacebookLoginOptions
Name    |   Type    |   Description
:--- |:--- |:--- 
auth_type|`string`|
scope|`string`|
return_scopes|`boolean`|
enable_profile_selector|`boolean`|
profile_selector_ids|`string`|

## FacebookLoginResponse
Name    |   Type    |   Description
:--- |:--- |:--- 
authResponse|`FacebookAuthResponse`|
status|`string`|
