---
name: Bookmarklets
tools: [Javascript]
image: https://png.pngtree.com/png-vector/20190423/ourmid/pngtree-bookmark-icon-vector-illustration-in-filled-style-for-any-purpose-png-image_975418.jpg
description: A collection of my custom bookmarklets.
---

# Bookmarklets

Bookmarklets are simple pieces of JavaScript code stored as bookmarks in your browser. They provide additional functionality to a page by manipulating its content or behavior. By clicking on a bookmarklet while on a specific web page, you can trigger the contained script to perform certain actions. On this page, you'll find some custom bookmarklets that I've written to make my life a little easier. :smile:

{% capture list_items %}
Compute Gradescope Raw Score
Count Google Calendar Hours
Extract YouTube Transcript
Remove GitHub Inline Comments
{% endcapture %}
{% include elements/list.html title="Table of Contents" type="toc" %}

## [Compute Gradescope Raw Score](javascript:var%20%24jscomp%3D%24jscomp%7C%7C%7B%7D%3B%24jscomp.scope%3D%7B%7D%3B%24jscomp.createTemplateTagFirstArg%3Dfunction(a)%7Breturn%20a.raw%3Da%7D%3B%24jscomp.createTemplateTagFirstArgWithRaw%3Dfunction(a%2Cb)%7Ba.raw%3Db%3Breturn%20a%7D%3B%24jscomp.arrayIteratorImpl%3Dfunction(a)%7Bvar%20b%3D0%3Breturn%20function()%7Breturn%20b%3Ca.length%3F%7Bdone%3A!1%2Cvalue%3Aa%5Bb%2B%2B%5D%7D%3A%7Bdone%3A!0%7D%7D%7D%3B%24jscomp.arrayIterator%3Dfunction(a)%7Breturn%7Bnext%3A%24jscomp.arrayIteratorImpl(a)%7D%7D%3B%24jscomp.makeIterator%3Dfunction(a)%7Bvar%20b%3D%22undefined%22!%3Dtypeof%20Symbol%26%26Symbol.iterator%26%26a%5BSymbol.iterator%5D%3Bif(b)return%20b.call(a)%3Bif(%22number%22%3D%3Dtypeof%20a.length)return%20%24jscomp.arrayIterator(a)%3Bthrow%20Error(String(a)%2B%22%20is%20not%20an%20iterable%20or%20ArrayLike%22)%3B%7D%3Bvar%20totalBeforeSlash%3D0%2CtotalAfterSlash%3D0%3Bdocument.querySelectorAll(%22.submissionStatus--score%22).forEach(function(a)%7Bvar%20b%3D%24jscomp.makeIterator(a.innerHTML.split(%22%20%2F%20%22))%3Ba%3Db.next().value%3Bb%3Db.next().value%3Ba%3DparseFloat(a)%3Bb%3DparseFloat(b)%3BtotalBeforeSlash%2B%3Da%3BtotalAfterSlash%2B%3Db%7D)%3Bvar%20percentage%3DtotalBeforeSlash%2FtotalAfterSlash*100%3Bpercentage%3DMath.round(100*percentage)%2F100%3Bvar%20alertMessage%3D%22The%20total%20is%20%22%2BtotalBeforeSlash%2B%22%20%2F%20%22%2BtotalAfterSlash%2B%22%20%3D%20%22%2Bpercentage%2B%22%25%22%3Balert(alertMessage)%3Bvoid+0)

(Drag this link to your bookmarks bar)

**Purpose**: Compute your raw total score on Gradescope.

**Usage**  
1. Open your Gradescope dashboard, where you can you see your assignments and their scores.
2. Click on this bookmarklet in your bookmarks bar.

![GitHub](/assets/projects/bookmarklet-gradescope.png)

---

## [Count Google Calendar Hours](javascript:var%20%24jscomp%3D%24jscomp%7C%7C%7B%7D%3B%24jscomp.scope%3D%7B%7D%3B%24jscomp.arrayIteratorImpl%3Dfunction(a)%7Bvar%20c%3D0%3Breturn%20function()%7Breturn%20c%3Ca.length%3F%7Bdone%3A!1%2Cvalue%3Aa%5Bc%2B%2B%5D%7D%3A%7Bdone%3A!0%7D%7D%7D%3B%24jscomp.arrayIterator%3Dfunction(a)%7Breturn%7Bnext%3A%24jscomp.arrayIteratorImpl(a)%7D%7D%3B%24jscomp.makeIterator%3Dfunction(a)%7Bvar%20c%3D%22undefined%22!%3Dtypeof%20Symbol%26%26Symbol.iterator%26%26a%5BSymbol.iterator%5D%3Bif(c)return%20c.call(a)%3Bif(%22number%22%3D%3Dtypeof%20a.length)return%20%24jscomp.arrayIterator(a)%3Bthrow%20Error(String(a)%2B%22%20is%20not%20an%20iterable%20or%20ArrayLike%22)%3B%7D%3Bvar%20reg%3D%2F(%5Cd%2B(%3A%5Cd%2B)%3F(am%7Cpm)%3F)%20%5Cu2013%20(%5Cd%2B(%3A%5Cd%2B)%3F(am%7Cpm))%2F%2Ctotal%3D0%3Bdocument.querySelectorAll(%22div%5Brole%3Dgridcell%5D%22).forEach(function(a)%7Ba%3Da.innerHTML%3Breg.test(a)%26%26(total%2B%3DdurationInHours(a))%7D)%3Balert(%22The%20total%20time%20on%20this%20search%20page%20is%20%22%2Btotal%2B%22%20hours!%22)%3Bfunction%20durationInHours(a)%7Ba%3Da.split(%22%20%5Cu2013%20%22)%3Bif(null%3D%3D%3Da%5B0%5D.match(%2Fam%7Cpm%2F))%7Bvar%20c%3Da%5B1%5D.match(%2Fam%7Cpm%2F)%3Ba%5B0%5D%2B%3Dc%5B0%5D%7Da%3Da.map(function(e)%7Bvar%20b%3De.match(%2F%5Cd%2B%3A%5Cd%2B%7C%5Cd%2B%2F)%5B0%5D%3Be%3De.match(%2Fam%7Cpm%2F)%5B0%5D%3Bvar%20d%3D%24jscomp.makeIterator(b.includes(%22%3A%22)%3Fb.split(%22%3A%22)%3A%5Bb%2C%2200%22%5D)%3Bb%3Dd.next().value%3Bd%3Dd.next().value%3Bb%3DparseInt(b)%3Bd%3DparseInt(d)%3B%22pm%22%3D%3D%3De%26%2612!%3D%3Db%26%26(b%2B%3D12)%3B%22am%22%3D%3D%3De%26%2612%3D%3D%3Db%26%26(b%3D0)%3Breturn%20b%2Bd%2F60%7D)%3Ba%3Da%5B1%5D-a%5B0%5D%3B0%3Ea%26%26(a%2B%3D24)%3Breturn%20a%7D%3Bvoid+0)

(Drag this link to your bookmarks bar)

**Purpose**: Compute the total hours of events that are displayed in a Google Calendar search. Useful for if you need to, say, add up your total hours doing a specific activity.

**Usage**  
1. Open Google Calendar and search for your desired events.
2. Click on this bookmarklet in your bookmarks bar.

![Calendar](/assets/projects/bookmarklet-calendar.png)

---

## [Extract YouTube Transcript](javascript:var%20elements%3Ddocument.querySelectorAll(%22yt-formatted-string.segment-text.style-scope.ytd-transcript-segment-renderer%22)%2Ctranscript%3D%22%22%3Belements.forEach(function(a)%7Btranscript%2B%3Da.textContent%2B%22%20%22%7D)%3Btranscript%3Dtranscript.replace(%2F%5Cn%2Fg%2C%22%20%22).trim()%3Bvar%20newWindow%3Dwindow.open(%22%22%2C%22_blank%22)%3BnewWindow.document.write(%22%3Chtml%3E%3Chead%3E%3Ctitle%3EYouTube%20Transcript%3C%2Ftitle%3E%3C%2Fhead%3E%3Cbody%3E%22)%3BnewWindow.document.write('%3Ctextarea%20style%3D%22width%3A100%25%3Bheight%3A100%25%3B%22%20readonly%3E')%3BnewWindow.document.write(transcript)%3BnewWindow.document.write(%22%3C%2Ftextarea%3E%22)%3BnewWindow.document.write(%22%3C%2Fbody%3E%3C%2Fhtml%3E%22)%3Bvoid+0)

(Drag this link to your bookmarks bar)

**Purpose**: Extract the full transcript from a YouTube video as plain text. Makes it easier to copy/paste the transcript without the timestamps getting in the way.

**Usage**  
1. Navigate to a YouTube video.
2. Open the video's transcript.
3. Click on this bookmarklet in your bookmarks bar.

![Transcript](/assets/projects/bookmarklet-youtube-transcript.png)

---

## [Remove GitHub Inline Comments](javascript:for(var%20elements%3Ddocument.querySelectorAll(%22.inline-comments%22)%2Ci%3D0%3Bi%3Celements.length%3Bi%2B%2B)elements%5Bi%5D.parentNode.removeChild(elements%5Bi%5D)%3Bvoid+0)

(Drag this link to your bookmarks bar)

**Purpose**: Remove the inline comments on a GitHub PR code page. Makes it easier to copy/paste the code, without the comments getting in the way.

**Usage**  
1. Open a GitHub PR that has inline comments.
2. Go to the `Files changed` tab.
3. Click on this bookmarklet in your bookmarks bar.

![GitHub](/assets/projects/bookmarklet-github.png)
