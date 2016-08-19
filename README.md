#### How to install (Chrome)

1. Download the project by clicking 'Download ZIP' on repository home page and extract the contents in some folder, or just clone the repository with `git clone`
2. (optional) Make your desired changes to the code
3. Open your browser and navigate to chrome://extensions/
4. Enable 'Developer mode'
5. Press 'Load unpacked extension' and select the folder where you extracted the contents of the project in step

#### How to install (Firefox)

1. Download the project by clicking 'Download ZIP' on repository home page and extract the contents in some folder, or just clone the repository with `git clone`
2. (optional) Make your desired changes to the code
3. Open Firefox and open a new tab with "about:debugging" on url-bar
4. Click "Load Temporary Add-on"
5. Search and open the "manifest.json" file you've downloaded and extracted
6. A new options button on will appear right next to "Menu" button


#### Quick confirmation for mass emails in gmail

If you're not authenticated you'll get one email per sell. This little script can be ran in console to get the confirmation links in a straightforward list. You can make it beautiful but really, since this is console-in-email you want to keep it KISS.

```
// create a new div
var e = document.createElement('div'); 
// open the email-convo, no need to click-to-expand duplicate mails (may need to for read mail but I didnt check)
// this searches for all <a> tags that have an url starting with the steam confirm link
var as = document.body.querySelectorAll('a[href^="https://steamcommunity.com/market/confirmlisting/"]');
// as is a "dom collection" and not a real array, this fixes that
var arr = Array.from(as); // es5: [].slice.call(arr,0) 
// steam uses near identical cancel links, compared to confirm only contains `cance=1` somewhere
// to KISS we just filter out urls containing `cancel`
arr = arr.filter(function(e) { return e.href.indexOf('cancel') < 0);
// for each link generate a new link using its url
arr = arr.map(function(e){ return '<a href="'+e.href+'">'+e.href+'</a><br>'});
// so now we have a list of `'<a href=steamlink>link</a><br>'`
// put the new clean links in the new div
e.innerHTML = arr.join('\n');
// add the div to the page. position irrelevant.
document.body.appendChild(e);
// push the div to the top and make sure you can see it. the next lines only set some css to the div
e.style.position = 'absolute';
e.style.top = 0;
e.style.backgroundColor='white';
e.style.border='1px solid black';
e.style.padding = '5px';
e.style.zIndex = 1000;
```

Then use ctrl+leftclick to open each link. They only need to open, steam doesn't really care about how rapid you do this (though they may rate limit you a little bit). Once it redirects to the market it should have confirmed the sell.

To remove the link, from same console do this:

```
e.parentNode.removeChild(e);
```

Other email environments probably need different scripts.
