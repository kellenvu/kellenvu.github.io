---
name: Bookmarklets
tools: [JavaScript]
image: https://png.pngtree.com/png-vector/20190423/ourmid/pngtree-bookmark-icon-vector-illustration-in-filled-style-for-any-purpose-png-image_975418.jpg
description: A collection of my custom bookmarklets.
---

# Bookmarklets

Bookmarklets are simple pieces of JavaScript code stored as bookmarks in your browser. They provide additional functionality to a page by manipulating its content or behavior. By clicking on a bookmarklet while on a specific web page, you can trigger the contained script to perform certain actions. Here, you'll find some custom bookmarklets that I've written to make my life a little easier. 🙂

{% capture list_items %}
Compute Gradescope Raw Score
Count Google Calendar Hours
Get Google Calendar Availability
Get Panopto Transcript
Get YouTube Transcript
Hide Retweets
Hide GitHub Inline Comments
Open Unread Canvas Grades
{% endcapture %}
{% include elements/list.html title="Table of Contents" type="toc" %}

## [Compute Gradescope Raw Score](javascript:(function()%7B%2F*%0AAdds%20up%20all%20the%20individual%20assignments%20and%20tell%20you%20the%20total%20score.%0A*%2F%0A%0Alet%20totalBeforeSlash%20%3D%200%3B%0Alet%20totalAfterSlash%20%3D%200%3B%0A%0Adocument.querySelectorAll('.submissionStatus--score').forEach((elem)%20%3D%3E%20%7B%0A%0A%09let%20str%20%3D%20elem.innerHTML%3B%0A%20%20%20%20let%20%5BbeforeSlash%2C%20afterSlash%5D%20%3D%20str.split('%20%2F%20')%3B%0A%0A%20%20%20%20%2F%2F%20Convert%20the%20strings%20to%20numbers%0A%20%20%20%20let%20numBeforeSlash%20%3D%20parseFloat(beforeSlash)%3B%0A%20%20%20%20let%20numAfterSlash%20%3D%20parseFloat(afterSlash)%3B%0A%0A%20%20%20%20%2F%2F%20Add%20the%20numbers%20to%20the%20running%20totals%0A%20%20%20%20totalBeforeSlash%20%2B%3D%20numBeforeSlash%3B%0A%20%20%20%20totalAfterSlash%20%2B%3D%20numAfterSlash%3B%0A%7D)%3B%0A%0Alet%20percentage%20%3D%20(totalBeforeSlash%20%2F%20totalAfterSlash)%20*%20100%3B%0Apercentage%20%3D%20Math.round(percentage%20*%20100)%20%2F%20100%3B%20%2F%2F%20Rounding%20to%20two%20decimal%20points%0A%0Alet%20alertMessage%20%3D%20%60The%20total%20is%20%24%7BtotalBeforeSlash%7D%20%2F%20%24%7BtotalAfterSlash%7D%20%3D%20%24%7Bpercentage%7D%25%60%3B%0Aalert(alertMessage)%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Computes your raw total score on Gradescope.

1. Open your Gradescope dashboard, where you can you see your assignments and their scores.
1. Click on this bookmarklet in your bookmarks bar.

![GitHub](/assets/projects/bookmarklet-gradescope.gif)

---

## [Count Google Calendar Hours](javascript:(function()%7B%2F*%0ARun%20this%20bookmarklet%20on%20the%20%22search%22%20page%20in%20Google%20Calendar.%0A%0AIt%20will%20detect%20all%20the%20time%20ranges%20on%20the%20page%2C%20and%20add%20up%20the%20total%20hours.%0A*%2F%0A%0Alet%20reg%20%3D%20%2F(%5Cd%2B(%3A%5Cd%2B)%3F(am%7Cpm)%3F)%20%E2%80%93%20(%5Cd%2B(%3A%5Cd%2B)%3F(am%7Cpm))%2F%3B%0Avar%20total%20%3D%200%3B%0A%0Adocument.querySelectorAll('div%5Brole%3Dgridcell%5D').forEach(ele%20%3D%3E%20%7B%0A%09let%20str%20%3D%20ele.innerHTML%3B%0A%09if(reg.test(str))%20%7B%0A%09%09total%20%2B%3D%20durationInHours(str)%3B%0A%09%7D%0A%7D)%3B%0A%0Aalert('The%20total%20time%20on%20this%20search%20page%20is%20'%20%2B%20total%20%2B%20'%20hours!')%3B%0A%0Afunction%20durationInHours(timeRange)%20%7B%0A%0A%20%20%20%20let%20parts%20%3D%20timeRange.split('%20%E2%80%93%20')%3B%0A%20%20%20%20if(parts%5B0%5D.match(%2Fam%7Cpm%2F)%20%3D%3D%3D%20null)%20%7B%0A%20%20%20%20%20%20%20%20let%20period%20%3D%20parts%5B1%5D.match(%2Fam%7Cpm%2F)%3B%0A%20%20%20%20%20%20%20%20parts%5B0%5D%20%2B%3D%20period%5B0%5D%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20let%20times%20%3D%20parts.map(part%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20%0A%20%20%20%20%20%20%20%20let%20timePart%20%3D%20part.match(%2F%5Cd%2B%3A%5Cd%2B%7C%5Cd%2B%2F)%5B0%5D%3B%20%0A%20%20%20%20%20%20%20%20let%20period%20%3D%20part.match(%2Fam%7Cpm%2F)%5B0%5D%3B%20%0A%0A%20%20%20%20%20%20%20%20let%20%5Bhour%2C%20minute%5D%20%3D%20timePart.includes('%3A')%20%3F%20timePart.split('%3A')%20%3A%20%5BtimePart%2C%20'00'%5D%3B%0A%20%20%20%20%20%20%20%20hour%20%3D%20parseInt(hour)%3B%0A%20%20%20%20%20%20%20%20minute%20%3D%20parseInt(minute)%3B%0A%0A%20%20%20%20%20%20%20%20if(period%20%3D%3D%3D%20'pm'%20%26%26%20hour%20!%3D%3D%2012)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20hour%20%2B%3D%2012%3B%0A%20%20%20%20%20%20%20%20%7D%0A%0A%20%20%20%20%20%20%20%20if(period%20%3D%3D%3D%20'am'%20%26%26%20hour%20%3D%3D%3D%2012)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20hour%20%3D%200%3B%0A%20%20%20%20%20%20%20%20%7D%0A%0A%20%20%20%20%20%20%20%20return%20hour%20%2B%20minute%20%2F%2060%3B%0A%20%20%20%20%7D)%3B%0A%0A%20%20%20%20let%20duration%20%3D%20times%5B1%5D%20-%20times%5B0%5D%3B%0A%20%20%20%20if(duration%20%3C%200)%20%7B%0A%20%20%20%20%20%20%20%20%2F%2F%20If%20the%20end%20time%20is%20before%20the%20start%20time%2C%20it%20means%20the%20time%20range%20crosses%20midnight.%0A%20%20%20%20%20%20%20%20%2F%2F%20Add%2024%20to%20the%20duration%20to%20correct%20this.%0A%20%20%20%20%20%20%20%20duration%20%2B%3D%2024%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20return%20duration%3B%0A%7D%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Computes the total hours of events that are displayed in a Google Calendar search. Useful for if you need to, say, add up your total hours doing a specific activity.

1. Open Google Calendar and search for your desired events.
1. Click on this bookmarklet in your bookmarks bar.

![Calendar](/assets/projects/bookmarklet-gcal-hours.gif)

---

## [Get Google Calendar Availability](javascript:(function()%7B%2F%2F%20Default%20settings%0Alet%20START_CONSTRAINT%20%3D%208%3B%20%20%20%2F%2F%20Earliest%20hour%20(e.g.%208%20%3D%208am)%0Alet%20END_CONSTRAINT%20%3D%2020%3B%20%20%20%20%2F%2F%20Latest%20hour%20(e.g.%2020%20%3D%208pm)%0Alet%20MIN_FREE_TIME%20%3D%2030%3B%20%20%20%20%20%2F%2F%20Minimum%20duration%20of%20a%20free%20block%20in%20minutes%0Alet%20BUFFER_MINUTES%20%3D%2015%3B%20%20%20%20%2F%2F%20Buffer%20time%20added%20before%20and%20after%20each%20event%20in%20minutes%0A%0A%2F%2F%20Prompt%20for%20user-defined%20settings%0Alet%20userInput%20%3D%20prompt(%0A%20%20%20%20%22SETTINGS%3A%5CnEarliest%20hour%20(e.g.%208%3D8am)%2C%20Latest%20hour%20(e.g.%2020%3D8pm)%2C%20Min%20free%20block%20(minutes)%2C%20Buffer%20around%20events%20(minutes)%22%2C%0A%20%20%20%20%60%24%7BSTART_CONSTRAINT%7D%2C%24%7BEND_CONSTRAINT%7D%2C%24%7BMIN_FREE_TIME%7D%2C%24%7BBUFFER_MINUTES%7D%60%0A)%3B%0A%0Aif%20(userInput)%20%7B%0A%20%20%20%20%5BSTART_CONSTRAINT%2C%20END_CONSTRAINT%2C%20MIN_FREE_TIME%2C%20BUFFER_MINUTES%5D%20%3D%20userInput.split('%2C').map(Number)%3B%0A%7D%0A%0A%2F%2F%20Event%20class%20representing%20a%20time%20interval%0Aclass%20Event%20%7B%0A%20%20%20%20constructor(start%2C%20end)%20%7B%0A%20%20%20%20%20%20%20%20this.start%20%3D%20start%3B%0A%20%20%20%20%20%20%20%20this.end%20%3D%20end%3B%0A%20%20%20%20%7D%0A%7D%0A%0A%2F**%0A%20*%20Parses%20a%20Google%20Calendar%20event%20string%20to%20an%20Event%20object.%0A%20*%20%40param%20%7Bstring%7D%20text%20-%20The%20text%20content%20of%20the%20calendar%20event%20div.%0A%20*%20%40returns%20%7BEvent%7Cnull%7D%20Parsed%20event%20or%20null%20if%20invalid.%0A%20*%2F%0Afunction%20parseTimeString(text)%20%7B%0A%0A%20%20%20%20const%20times%20%3D%20text.match(%2F%5Cd%2B(%3A%5Cd%2B)%3F(am%7Cpm)%2Fgi)%3B%0A%20%20%20%20const%20date%20%3D%20text.match(%2F%5CS%2B%20%5Cd%7B1%2C2%7D%2C%20%5Cd%7B4%7D%24%2Fg)%3F.%5B0%5D%3B%0A%20%20%20%20if%20(!times%20%7C%7C%20!date)%20return%20null%3B%0A%0A%20%20%20%20const%20start%20%3D%20new%20Date(%60%24%7Bdate%7D%20%24%7BconvertTo24h(times%5B0%5D)%7D%60)%3B%0A%20%20%20%20const%20end%20%3D%20new%20Date(%60%24%7Bdate%7D%20%24%7BconvertTo24h(times%5B1%5D%20%7C%7C%20times%5B0%5D)%7D%60)%3B%0A%20%20%20%20return%20end%20%3E%20start%20%3F%20new%20Event(start%2C%20end)%20%3A%20null%3B%0A%7D%0A%0A%2F**%0A%20*%20Converts%20a%2012-hour%20time%20string%20to%2024-hour%20format.%0A%20*%20%40param%20%7Bstring%7D%20timeStr%20-%20Time%20string%20like%20%221%3A30pm%22%20or%20%2212am%22.%0A%20*%20%40returns%20%7Bstring%7D%2024-hour%20formatted%20time%20(e.g.%2C%20%2213%3A30%22).%0A%20*%2F%0Afunction%20convertTo24h(timeStr)%20%7B%0A%20%20%20%20let%20%5Btime%2C%20period%5D%20%3D%20timeStr.toLowerCase().split(%2F(am%7Cpm)%2F)%3B%0A%20%20%20%20let%20%5Bh%2C%20m%5D%20%3D%20time.split('%3A').map(Number)%3B%0A%20%20%20%20if%20(!m)%20m%20%3D%200%3B%0A%20%20%20%20if%20(period%20%3D%3D%3D%20'pm'%20%26%26%20h%20!%3D%3D%2012)%20h%20%2B%3D%2012%3B%0A%20%20%20%20if%20(period%20%3D%3D%3D%20'am'%20%26%26%20h%20%3D%3D%3D%2012)%20h%20%3D%200%3B%0A%20%20%20%20return%20%60%24%7Bh.toString().padStart(2%2C%20'0')%7D%3A%24%7Bm.toString().padStart(2%2C%20'0')%7D%60%3B%0A%7D%0A%0A%2F**%0A%20*%20Extracts%20direct%20text%20(not%20children)%20from%20an%20HTML%20element.%0A%20*%20%40param%20%7BElement%7D%20el%20-%20The%20HTML%20element.%0A%20*%20%40returns%20%7Bstring%7D%20Concatenated%20text%20content.%0A%20*%2F%0Afunction%20getTextContent(el)%20%7B%0A%20%20%20%20return%20Array.from(el.childNodes)%0A%20%20%20%20%20%20%20%20.filter(n%20%3D%3E%20n.nodeType%20%3D%3D%3D%20Node.TEXT_NODE)%0A%20%20%20%20%20%20%20%20.map(n%20%3D%3E%20n.textContent.trim())%0A%20%20%20%20%20%20%20%20.join('')%3B%0A%7D%0A%0A%2F**%0A%20*%20Subtracts%20a%20time%20block%20from%20an%20array%20of%20available%20intervals.%0A%20*%20%40param%20%7BEvent%5B%5D%7D%20available%20-%20List%20of%20currently%20available%20time%20blocks.%0A%20*%20%40param%20%7BEvent%7D%20block%20-%20Time%20block%20to%20subtract.%0A%20*%20%40returns%20%7BEvent%5B%5D%7D%20Updated%20list%20of%20available%20blocks.%0A%20*%2F%0Afunction%20subtractIntervals(available%2C%20block)%20%7B%0A%0A%20%20%20%20const%20result%20%3D%20%5B%5D%3B%0A%0A%20%20%20%20for%20(let%20interval%20of%20available)%20%7B%0A%0A%20%20%20%20%20%20%20%20if%20(block.end%20%3C%3D%20interval.start%20%7C%7C%20block.start%20%3E%3D%20interval.end)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20result.push(interval)%3B%0A%20%20%20%20%20%20%20%20%20%20%20%20continue%3B%0A%20%20%20%20%20%20%20%20%7D%0A%0A%20%20%20%20%20%20%20%20if%20(block.start%20%3E%20interval.start)%0A%20%20%20%20%20%20%20%20%20%20%20%20result.push(new%20Event(interval.start%2C%20block.start))%3B%0A%0A%20%20%20%20%20%20%20%20if%20(block.end%20%3C%20interval.end)%0A%20%20%20%20%20%20%20%20%20%20%20%20result.push(new%20Event(block.end%2C%20interval.end))%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20return%20result%3B%0A%7D%0A%0A%2F**%0A%20*%20Generates%20one%20full%20block%20per%20day%20between%20START%20and%20END%20constraints.%0A%20*%20%40param%20%7BDate%7D%20startDate%20-%20The%20first%20day%20to%20consider.%0A%20*%20%40param%20%7Bnumber%7D%20days%20-%20Number%20of%20days%20to%20generate.%0A%20*%20%40returns%20%7BEvent%5B%5D%7D%20Array%20of%20full-day%20availability%20blocks.%0A%20*%2F%0Afunction%20getInitialFreeBlocks(startDate%2C%20days)%20%7B%0A%0A%20%20%20%20const%20blocks%20%3D%20%5B%5D%3B%0A%0A%20%20%20%20for%20(let%20i%20%3D%200%3B%20i%20%3C%20days%3B%20i%2B%2B)%20%7B%0A%20%20%20%20%20%20%20%20const%20day%20%3D%20new%20Date(startDate)%3B%0A%20%20%20%20%20%20%20%20day.setDate(day.getDate()%20%2B%20i)%3B%0A%20%20%20%20%20%20%20%20const%20start%20%3D%20new%20Date(day)%3B%0A%20%20%20%20%20%20%20%20const%20end%20%3D%20new%20Date(day)%3B%0A%20%20%20%20%20%20%20%20start.setHours(START_CONSTRAINT%2C%200%2C%200%2C%200)%3B%0A%20%20%20%20%20%20%20%20end.setHours(END_CONSTRAINT%2C%200%2C%200%2C%200)%3B%0A%20%20%20%20%20%20%20%20blocks.push(new%20Event(start%2C%20end))%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20return%20blocks%3B%0A%7D%0A%0A%2F**%0A%20*%20Expands%20an%20event%20block%20with%20buffer%20on%20both%20sides.%0A%20*%20%40param%20%7BEvent%7D%20event%20-%20The%20original%20event.%0A%20*%20%40param%20%7Bnumber%7D%20bufferMinutes%20-%20Buffer%20in%20minutes.%0A%20*%20%40returns%20%7BEvent%7D%20Buffered%20event%20block.%0A%20*%2F%0Afunction%20applyBuffer(event%2C%20bufferMinutes)%20%7B%0A%20%20%20%20const%20bufferedStart%20%3D%20new%20Date(event.start)%3B%0A%20%20%20%20const%20bufferedEnd%20%3D%20new%20Date(event.end)%3B%0A%20%20%20%20bufferedStart.setMinutes(bufferedStart.getMinutes()%20-%20bufferMinutes)%3B%0A%20%20%20%20bufferedEnd.setMinutes(bufferedEnd.getMinutes()%20%2B%20bufferMinutes)%3B%0A%20%20%20%20return%20new%20Event(bufferedStart%2C%20bufferedEnd)%3B%0A%7D%0A%0A%2F**%0A%20*%20Formats%20the%20list%20of%20free%20blocks%20by%20date%20for%20display.%0A%20*%20%40param%20%7BEvent%5B%5D%7D%20freeBlocks%20-%20Available%20free%20time%20blocks.%0A%20*%20%40returns%20%7Bstring%7D%20Formatted%20summary%20of%20free%20time.%0A%20*%2F%0Afunction%20formatFreeTime(freeBlocks)%20%7B%0A%0A%20%20%20%20const%20byDay%20%3D%20%7B%7D%3B%0A%0A%20%20%20%20for%20(let%20block%20of%20freeBlocks)%20%7B%0A%20%20%20%20%20%20%20%20const%20date%20%3D%20block.start.toLocaleDateString('en-US'%2C%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20weekday%3A%20'short'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20month%3A%20'long'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20day%3A%20'numeric'%0A%20%20%20%20%20%20%20%20%7D)%3B%0A%20%20%20%20%20%20%20%20const%20start%20%3D%20block.start.toLocaleTimeString('en-US'%2C%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20hour%3A%20'numeric'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20minute%3A%20'2-digit'%0A%20%20%20%20%20%20%20%20%7D).toLowerCase()%3B%0A%20%20%20%20%20%20%20%20const%20end%20%3D%20block.end.toLocaleTimeString('en-US'%2C%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20hour%3A%20'numeric'%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20minute%3A%20'2-digit'%0A%20%20%20%20%20%20%20%20%7D).toLowerCase()%3B%0A%20%20%20%20%20%20%20%20byDay%5Bdate%5D%20%3D%20byDay%5Bdate%5D%20%7C%7C%20%5B%5D%3B%0A%20%20%20%20%20%20%20%20byDay%5Bdate%5D.push(%60%24%7Bstart%7D%E2%80%93%24%7Bend%7D%60)%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20let%20out%20%3D%20'Availability%3A%5Cn%5Cn'%3B%0A%0A%20%20%20%20for%20(let%20%5Bdate%2C%20blocks%5D%20of%20Object.entries(byDay))%20%7B%0A%20%20%20%20%20%20%20%20out%20%2B%3D%20%60%24%7Bdate%7D%5Cn%24%7Bblocks.join('%5Cn')%20%7C%7C%20'n%2Fa'%7D%5Cn%5Cn%60%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20return%20out%3B%0A%7D%0A%0A%2F%2F%20MAIN%20EXECUTION%0A%0A%2F%2F%20Parse%20visible%20calendar%20events%0Aconst%20eventDivs%20%3D%20document.querySelectorAll('div%5Brole%3D%22gridcell%22%5D%20%3E%20div%20%3E%20div%5Brole%3D%22button%22%5D%20%3E%20div')%3B%0Aconst%20events%20%3D%20Array.from(eventDivs)%0A%20%20%20%20.map(div%20%3D%3E%20parseTimeString(getTextContent(div)))%0A%20%20%20%20.filter(Boolean)%3B%0A%0A%2F%2F%20Extract%20visible%20date%20range%20from%20page%20header%0Aconst%20header%20%3D%20document.querySelector('div%5Brole%3D%22main%22%5D%20%3E%20h1')%3B%0Aconst%20ariaLabel%20%3D%20header%3F.getAttribute('aria-label')%20%7C%7C%20''%3B%0Alet%20startDate%20%3D%20null%3B%0Alet%20numberOfDays%20%3D%207%3B%0A%0Aconst%20match%20%3D%20ariaLabel.match(%2F(%5Cd%2B)%20days%2C%20starting%20(%5BA-Za-z%5D%2B%2C%20.%2B%3F)%2C%20%5Cd%2B%20events%2F)%3B%0Aif%20(match)%20%7B%0A%20%20%20%20numberOfDays%20%3D%20parseInt(match%5B1%5D%2C%2010)%3B%0A%20%20%20%20startDate%20%3D%20new%20Date(match%5B2%5D)%3B%0A%7D%20else%20%7B%0A%20%20%20%20const%20weekMatch%20%3D%20ariaLabel.match(%2FWeek%20of%20(%5BA-Za-z%5D%2B%20%5Cd%7B1%2C2%7D%2C%20%5Cd%7B4%7D)%2C%20%5Cd%2B%20events%2F)%3B%0A%20%20%20%20if%20(weekMatch)%20%7B%0A%20%20%20%20%20%20%20%20startDate%20%3D%20new%20Date(weekMatch%5B1%5D)%3B%0A%20%20%20%20%20%20%20%20numberOfDays%20%3D%207%3B%0A%20%20%20%20%7D%0A%7D%0A%0Aif%20(!startDate)%20%7B%0A%20%20%20%20alert(%22Could%20not%20determine%20visible%20date%20range.%22)%3B%0A%20%20%20%20throw%20new%20Error(%22Missing%20startDate%22)%3B%0A%7D%0A%0A%2F%2F%20Step%201%3A%20Start%20with%20full%20availability%20per%20day%0Alet%20freeBlocks%20%3D%20getInitialFreeBlocks(startDate%2C%20numberOfDays)%3B%0A%0A%2F%2F%20Step%202%3A%20Subtract%20out%20each%20buffered%20event%20from%20availability%0Afor%20(const%20event%20of%20events)%20%7B%0A%20%20%20%20const%20bufferedEvent%20%3D%20applyBuffer(event%2C%20BUFFER_MINUTES)%3B%0A%20%20%20%20freeBlocks%20%3D%20subtractIntervals(freeBlocks%2C%20bufferedEvent)%3B%0A%7D%0A%0A%2F%2F%20Step%203%3A%20Filter%20out%20short%20blocks%0AfreeBlocks%20%3D%20freeBlocks.filter(b%20%3D%3E%20(b.end%20-%20b.start)%20%3E%3D%20MIN_FREE_TIME%20*%2060%20*%201000)%3B%0A%0A%2F%2F%20Step%204%3A%20Format%20and%20display%20the%20availability%0Aconst%20availabilityText%20%3D%20formatFreeTime(freeBlocks)%3B%0A%0Alet%20displayDiv%20%3D%20document.getElementById('computed-availability')%3B%0Aif%20(!displayDiv)%20%7B%0A%20%20%20%20displayDiv%20%3D%20document.createElement('div')%3B%0A%20%20%20%20displayDiv.id%20%3D%20'computed-availability'%3B%0A%20%20%20%20displayDiv.style.whiteSpace%20%3D%20'pre-wrap'%3B%0A%20%20%20%20displayDiv.style.padding%20%3D%20'10px'%3B%0A%20%20%20%20displayDiv.style.marginBottom%20%3D%20'20px'%3B%0A%20%20%20%20displayDiv.style.backgroundColor%20%3D%20'%23f9f9f9'%3B%0A%20%20%20%20const%20target%20%3D%20document.getElementById('drawerMiniMonthNavigator')%3B%0A%20%20%20%20if%20(target)%20target.parentNode.insertBefore(displayDiv%2C%20target)%3B%0A%7D%0A%0AdisplayDiv.textContent%20%3D%20availabilityText%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Reads your Google Calendar and outputs your availability in plain text. Makes it easy to tell someone over, say, email what times you're available to meet.

1. Navigate to the Google Calendar **week view**.
1. Activate your desired calendars (whatever events are currently showing on the screen are the time blocks when you are "busy").
1. Click on this bookmarklet in your bookmarks bar.
1. Modify the settings as desired, then click OK.

![Calendar](/assets/projects/bookmarklet-gcal-availability.gif)

---

## [Get Panopto Transcript](javascript:(function()%7B%2F**%0A%20*%20Go%20to%20a%20Panopto%20video.%0A%20*%20Click%20the%20%22Captions%22%20button.%0A%20*%20Run%20this%20bookmarklet.%0A%20*%20It%20will%20open%20a%20new%20tab%20with%20the%20transcript.%0A%20*%2F%0A%0Alet%20rows%20%3D%20document.querySelectorAll(%22div.index-event-row%22)%3B%0Alet%20transcript%20%3D%20%22%22%3B%0A%0Arows.forEach((row)%20%3D%3E%20%7B%0A%0A%20%20%20%20if%20(!row.querySelector('div%5Baria-label%3D%22User%20Created%20Transcript%22%5D'))%20%7B%0A%20%20%20%20%20%20%20%20return%3B%0A%20%20%20%20%7D%0A%0A%20%20%20%20let%20captionSpan%20%3D%20row.querySelector(%22div.event-text%20%3E%20span%22)%3B%0A%20%20%20%20if%20(captionSpan)%20%7B%0A%20%20%20%20%20%20%20%20transcript%20%2B%3D%20captionSpan.innerHTML.trim()%20%2B%20%22%20%22%3B%0A%20%20%20%20%7D%0A%7D)%3B%0A%0Atranscript%20%3D%20transcript.replace(%2F%5Cn%2Fg%2C%20%22%20%22).trim()%3B%0A%0Alet%20htmlContent%20%3D%20%60%0A%3Chtml%3E%0A%3Chead%3E%0A%20%20%20%20%3Ctitle%3ETranscript%3C%2Ftitle%3E%0A%3C%2Fhead%3E%0A%3Cbody%3E%0A%20%20%20%20%3Cdiv%20style%3D%22white-space%3A%20pre-wrap%3B%22%3E%24%7Btranscript%7D%3C%2Fdiv%3E%0A%3C%2Fbody%3E%0A%3C%2Fhtml%3E%60%3B%0A%0Alet%20blob%20%3D%20new%20Blob(%5BhtmlContent%5D%2C%20%7B%20type%3A%20'text%2Fhtml'%20%7D)%3B%0Alet%20url%20%3D%20URL.createObjectURL(blob)%3B%0Awindow.open(url%2C%20%22_blank%22)%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Extracts the full transcript from a Panopto video as plain text. Makes it easier to copy/paste the transcript.

1. Navigate to a Panopto video.
1. Open the video's Captions tab.
1. Click on this bookmarklet in your bookmarks bar.

![Panopto transcript](/assets/projects/bookmarklet-panopto-transcript.gif)

---

## [Get YouTube Transcript](javascript:(function()%7B%2F**%0A%20*%20Go%20to%20a%20YouTube%20video.%0A%20*%20Click%20the%20%22Show%20transcript%22%20button.%0A%20*%20Run%20this%20bookmarklet.%0A%20*%20It%20will%20open%20a%20new%20tab%20with%20the%20transcript.%0A%20*%2F%0A%0Alet%20elements%20%3D%20document.querySelectorAll('yt-formatted-string.segment-text.style-scope.ytd-transcript-segment-renderer')%3B%0Alet%20transcript%20%3D%20%22%22%3B%0A%0Aelements.forEach((elem)%20%3D%3E%20%7B%0A%20%20%20%20transcript%20%2B%3D%20elem.innerHTML%20%2B%20%22%20%22%3B%0A%7D)%3B%0A%0Atranscript%20%3D%20transcript.replace(%2F%5Cn%2Fg%2C%20%22%20%22).trim()%3B%0A%0Alet%20htmlContent%20%3D%20%60%0A%3Chtml%3E%0A%3Chead%3E%0A%20%20%20%20%3Ctitle%3ETranscript%3C%2Ftitle%3E%0A%3C%2Fhead%3E%0A%3Cbody%3E%0A%20%20%20%20%3Cdiv%20style%3D%22white-space%3A%20pre-wrap%3B%22%3E%24%7Btranscript%7D%3C%2Fdiv%3E%0A%3C%2Fbody%3E%0A%3C%2Fhtml%3E%60%3B%0A%0Alet%20blob%20%3D%20new%20Blob(%5BhtmlContent%5D%2C%20%7B%20type%3A%20'text%2Fhtml'%20%7D)%3B%0Alet%20url%20%3D%20URL.createObjectURL(blob)%3B%0Awindow.open(url%2C%20%22_blank%22)%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Extracts the full transcript from a YouTube video as plain text. Makes it easier to copy/paste the transcript.

1. Navigate to a YouTube video.
1. Open the video's transcript.
1. Click on this bookmarklet in your bookmarks bar.

![YouTube transcript](/assets/projects/bookmarklet-youtube-transcript.gif)

---

## [Hide Retweets](javascript:(function()%7B%2F**%0A%20*%20Continuously%20checks%20the%20page%20for%20any%20reposted%20tweets%2C%20and%20hides%20them.%0A%20*%2F%0A%0Afunction%20hideRetweetDivs()%20%7B%0A%0A%20%20%20%20var%20elems%20%3D%20document.querySelectorAll('div%5Bdata-testid%3D%22cellInnerDiv%22%5D')%3B%0A%0A%20%20%20%20Array.from(elems).forEach((elem)%20%3D%3E%20%7B%0A%20%20%20%20%20%20%20%20if%20(elem.textContent.includes('reposted'))%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20elem.style.display%20%3D%20'none'%3B%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D)%0A%7D%0A%0AsetInterval(hideRetweetDivs%2C%201E3)%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: When viewing a Twitter feed (either your own feed or a user's timeline), this bookmarklet hides all of the reposts.

1. Go to your [Twitter home feed](https://twitter.com/home) or a user's profile.
1. Click on this bookmarklet in your bookmarks bar.
1. Any tweets that were reposted are now hidden (you might see them flash on screen for a bit before they disappear).

![Hide retweets](/assets/projects/bookmarklet-hide-retweets.gif)

---

## [Hide GitHub Inline Comments](javascript:(function()%7B%2F**%0A%20*%20Run%20this%20bookmarklet%20on%20a%20GitHub%20code%20page.%20It%20will%20remove%20all%20of%20the%20inline%20comments%2C%20making%20it%20easier%20to%20copy%2Fpaste.%0A%20*%2F%0A%0Avar%20elements%20%3D%20document.querySelectorAll('.inline-comments')%3B%0Aelements.forEach((elem)%20%3D%3E%20%7B%0A%20%20%20%20elem.parentNode.removeChild(elem)%3B%0A%7D)%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Hides the inline comments on a GitHub PR code page. Makes it easier to copy/paste the code without the comments getting in the way. The comments will return when you refresh the page.

1. Open a GitHub PR that has inline comments.
1. Go to the `Files changed` tab.
1. Click on this bookmarklet in your bookmarks bar.

![GitHub](/assets/projects/bookmarklet-hide-github.gif)

---

## [Open Unread Canvas Grades](javascript:(function()%7B%2F*%0AFinds%20all%20unread%20grade%20notifications%20on%20Canvas%20Grades%20page%20and%20opens%20each%20associated%20assignment%20in%20a%20new%20tab.%20Make%20sure%20to%20click%20%22allow%20pop-ups%22%20when%20you%20run%20this.%0A*%2F%0A%0Adocument.querySelectorAll(%22span.unread_dot.grade_dot%22).forEach((dot)%20%3D%3E%20%7B%0A%0A%20%20%20%20let%20parent%20%3D%20dot%3B%0A%0A%20%20%20%20for%20(let%20i%20%3D%200%3B%20i%20%3C%204%3B%20i%2B%2B)%20%7B%0A%20%20%20%20%20%20%20%20if%20(parent.parentElement)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20parent%20%3D%20parent.parentElement%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%0A%20%20%20%20let%20titleElem%20%3D%20parent.querySelector(%22.title%22)%3B%0A%20%20%20%20if%20(titleElem)%20%7B%0A%20%20%20%20%20%20%20%20let%20link%20%3D%20titleElem.querySelector(%22a%22)%3B%0A%20%20%20%20%20%20%20%20if%20(link%20%26%26%20link.href)%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20window.open(link.href%2C%20%22_blank%22)%3B%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%7D)%3B%7D)()%3B)

(Drag this link to your bookmarks bar)

**Purpose**: Automatically clicks all the unread graded assignments on the Canvas `Grades` page, in order to remove the notification bubble.

1. Open the Canvas `Grades` page.
1. Click on this bookmarklet in your bookmarks bar.
1. If multiple pages are not opening, then click "Allow Pop-Ups" in your browser.
