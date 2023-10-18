---
title: How to integrate Siri with Notion for Free
tags: [Productivity, Tutorial]
description: Use your voice to add content to Notion!
---

**[Notion](https://www.notion.so/)** is one of the most powerful productivity apps around, but it's missing a key feature: it doesn't natively integrate with Apple's automation app, **Shortcuts**.

Some third-party services like [Natuomate](https://www.nautomate.app/) have been developed to fill that gap, letting you add content to your Notion databases automatically—but they cost **money**.

Here, I will show you how to integrate Shortcuts with Notion at **no cost**. By the end of this tutorial, you should be able to add content to your Notion page with a simple **Siri voice command**.

---

## Step 1: Create Your Notion Database

First, I'll describe how I set up my Notion database. If you're already happy with your Notion database, skip to step 2!

Personally, I use Notion as a **todo list**. I like the Kanban board layout, where I categorize tasks as either **High Priority**, **Low Priority**, or **Done**.

<img src="/assets/posts/notion-kanban.png" width="800px">

Something that annoyed me about the default Kanban template was that the `Done` list would pile up with completed tasks. To fix this, I created a filter to only show tasks completed in the **last 24 hours**.

I gave each task 3 properties:

- **Status**: A Select property that is either `High Priority`, `Low Priority`, or `Done`
- **Last Edited**: One of the default properties
- **Show?**: A Formula property with the following formula

```
or(prop("Status") != "Done!", dateBetween(now(), prop("Last Edited"), "hours") < 24)
```

Then I added a filter to only show tasks where the `Show?` property is true.

You can make a copy of my Notion template [here](https://lying-tent-403.notion.site/Task-Template-e5ed1ec9fb964274b81e00901b4c161e).

## Step 2: Set Up the Integration

Go to [https://www.notion.so/my-integrations](https://www.notion.so/my-integrations) and make a new integration. Give it any name and the following capabilities:

<img src="/assets/posts/notion-capabilities.png" width="400px">

Go to the `Secrets` tab. You should see an `Internal Integration Secret`. We will use this later.

<img src="/assets/posts/notion-secret.png" width="700px">

Go to the page that contains your Notion database and click `Open as full page`.

<img src="/assets/posts/notion-open-as-full-page.png" width="700px">

Examine the URL of this page. It should look something like `https://www.notion.so/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx?v=yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy`. Take note of the `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` part—this is the **database ID**.

Click the meatballs menu in the top right, and click `Add connections`. Search for the name of the integration that you created earlier, and add it.

<img src="/assets/posts/notion-connections.png" width="700px">

At this point, you have successfully created an integration! Anyone with the internal integration secret and the database ID will be able to POST content to this database, or GET content from it, using an [API request](https://developers.notion.com/reference/post-page).

For example, you could POST a new task to my Kanban template by running the following Python code:

