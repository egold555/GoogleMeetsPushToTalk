# GoogleMeetsPushToTalk
Simple tampermonkey script to add a push to talk feature to google hangouts.

## Tampermonkey
```javascript
// ==UserScript==
// @name         Google Hangouts PTT
// @version      1.0
// @description  Hold down Space key to talk, let go to mute.
// @author       Eric Golde
// @match        https://meet.google.com/*
// @grant        none
// ==/UserScript==

(() => {
	var el = undefined;
	const mic = en => ({key,repeat,target}) => {
		el && el.isConnected || (el = document.querySelector('[data-is-muted][role="button"]'));
		el && key===' ' && !repeat && !('value' in target) && el.dataset.isMuted === String(en) && el.click()
	}
	document.body.addEventListener('keydown', mic(true))
	document.body.addEventListener('keyup', mic(false))
})();
```

## Paste into console
```javascript
var el = undefined;
const mic = en => ({key,repeat,target}) => {
	el && el.isConnected || (el = document.querySelector('[data-is-muted][role="button"]'));
	el && key===' ' && !repeat && !('value' in target) && el.dataset.isMuted === String(en) && el.click()
}
document.body.addEventListener('keydown', mic(true))
document.body.addEventListener('keyup', mic(false))
```
