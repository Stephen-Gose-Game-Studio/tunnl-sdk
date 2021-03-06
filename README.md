[![npm](https://img.shields.io/npm/v/npm.svg)](https://nodejs.org/)
[![GitHub version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/GameDistribution/TUNNL-SDK/)
[![Built with Grunt](https://cdn.gruntjs.com/builtwith.svg)](http://gruntjs.com/)
[![license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/GameDistribution/TUNNL-SDK/blob/master/LICENSE)


# Tunnl.com Advertisement SDK
This is the documentation of the "Tunnl.com Advertisement SDK" project.

Monetization, game, video distribution and more.

Running into any issues? Check out the F.A.Q. within the Wiki of the github repository before mailing to <a href="info@tunnl.com" target="_blank">info@tunnl.com</a>

## Implementation 
The SDK should be integrated within the web page itself by loading it through our CDN. Specific information of the SDK features and usages can be found at the <a href="https://github.com/gamedistribution/tunnl-sdk/wiki" target="_blank">wiki</a>.

### CDN
Add the following script to your document.
```
window["TUNNL_OPTIONS"] = {
    "debug": false,
    "container": "preroll",
    "onEvent": function(event) {
        switch (event.name) {
            case "SDK_CONTENT_START":
                // ...
                break;
            case "SDK_CONTENT_PAUSE":
                // ...
                break;
            case "SDK_READY":
                // ...
                break;
            case "SDK_ERROR":
                // ...
                break;
        }
    },
};
(function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s);
    js.id = id;
    js.src = '//preroll.api.gamedistribution.com/preroll/main.min.js';
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'tunnl-jssdk'));
```

### Legacy - Don't use this, only available for old implementations.
The ./index_legacy.html of this project contains a legacy integration example of the old SDK. Don't use this anymore.
```
//preroll.api.gamedistribution.com/preroll/libs/gd/api.js
//preroll.api.gamedistribution.com/preroll/libs/gd/api.min.js

```

## Debugging
Pages, which include the SDK, can be easily debugged by calling the following from a browser developer console:
```
tunnl.openConsole();
```

## Repository
The SDK is maintained on a public github repository.
<a href="https://github.com/gamedistribution/tunnl-sdk" target="_blank">https://github.com/gamedistribution/tunnl-sdk</a>

## Deployment
Deployment of the SDK to production environments is done through TeamCity.

## Installation for development
Install the following programs:
* [NodeJS LTS](https://nodejs.org/).
* [Grunt](http://gruntjs.com/).

Pull in the rest of the requirements using npm:
```
npm install
```

Setup a local node server, watch changes and update your browser view automatically:
```
grunt
```

Make a production build for the CDN solution. The npmjs version uses a "prepublish"-task defined within package.json, which does a simple babel task, similar to this task:
```
grunt build
```

## Events
### SDK EVENTS
The SDK events should be used by developers to start or pause their game or handling critical errors. Unless the errors are ad related, then they could hook into the AD_ERROR event, however; the SDK should gracefully fail, so this should not be needed.

| Event | Description |
| --- | --- |
| SDK_READY | When the SDK is ready. |
| SDK_ERROR | When the SDK has hit a critical error. |
| SDK_CONTENT_START | When the game should start. |
| SDK_CONTENT_PAUSE | When the game should pause. |

### IMA SDK EVENTS
The SDK events are custom ads for handling any thing related to the IMA SDK itself.

| Event | Description |
| --- | --- |
| AD_SDK_LOADER_READY | When the adsLoader instance is ready to create an adsManager instance |
| AD_SDK_MANAGER_READY | When the adsManager instance is ready with ads. |
| AD_SDK_REQUEST_ADS | When new ads are requested. |
| AD_SDK_ERROR | When the SDK hits a critical error. |
| AD_SDK_FINISHED | When the SDK is finished running the ad. |
| AD_CANCELED | When the ad is cancelled or stopped because its done running an ad. |
| AD_SAFETY_TIMER | When the safety timer is cleared. We run this timer to make sure the SDK and ads do not stop us from starting the game after, whenever there is a weird error. |

### AD EVENTS
The SDK uses the IMA SDK for loading ads. All events of this SDK are also available to the developer.
https://developers.google.com/interactive-media-ads/docs/sdks/html5/

| Event | Description |
| --- | --- |
| AD_ERROR | When the ad it self has an error. | 
| AD_BREAK_READY | Fired when an ad rule or a VMAP ad break would have played if autoPlayAdBreaks is false. |
| AD_METADATA | Fired when an ads list is loaded. |
| ALL_ADS_COMPLETED | Fired when the ads manager is done playing all the ads. |
| CLICK | Fired when the ad is clicked. |
| COMPLETE | Fired when the ad completes playing. |
| CONTENT_PAUSE_REQUESTED | Fired when content should be paused. This usually happens right before an ad is about to cover the content. |
| CONTENT_RESUME_REQUESTED | Fired when content should be resumed. This usually happens when an ad finishes or collapses. |
| DURATION_CHANGE | Fired when the ad's duration changes. |
| FIRST_QUARTILE | Fired when the ad playhead crosses first quartile. |
| IMPRESSION | Fired when the impression URL has been pinged. |
| INTERACTION | Fired when an ad triggers the interaction callback. Ad interactions contain an interaction ID string in the ad data. |
| LINEAR_CHANGED | Fired when the displayed ad changes from linear to nonlinear, or vice versa. |
| LOADED | Fired when ad data is available. |
| LOG | Fired when a non-fatal error is encountered. The user need not take any action since the SDK will continue with the same or next ad playback depending on the error situation. |
| MIDPOINT | Fired when the ad playhead crosses midpoint. |
| PAUSED | Fired when the ad is paused. |
| RESUMED | Fired when the ad is resumed. |
| SKIPPABLE_STATE_CHANGED | Fired when the displayed ads skippable state is changed. |
| SKIPPED | Fired when the ad is skipped by the user. |
| STARTED | Fired when the ad starts playing. |
| THIRD_QUARTILE | Fired when the ad playhead crosses third quartile. |
| USER_CLOSE | Fired when the ad is closed by the user. |
| VOLUME_CHANGED | Fired when the ad volume has changed. |
| VOLUME_MUTED | Fired when the ad volume has been muted. |



	

	

	

	

	
