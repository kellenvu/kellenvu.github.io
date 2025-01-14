---
title: How to integrate Siri with Notion for free
tags: [Productivity, Guide]
description: Use your voice to add content to Notion.
comments: true
---

**[Notion](https://www.notion.so/)** is one of the most powerful productivity apps around, but it's missing a key feature: it doesn't natively integrate with Apple's automation app, **Shortcuts**.

Some third-party services like [Nautomate](https://www.nautomate.app/) have been developed to fill that gap, letting you add content to your Notion databases automatically—but they cost **money**.

Here, I will show you how to integrate Shortcuts with Notion at **no cost**. By the end of this guide, you should be able to add content to your Notion page with a simple **Siri voice command**.

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

<iframe class="my-3" src="https://www.iorad.com/player/2496222/Add-an-integration-to-Notion?src=iframe&oembed=1" width="100%" height="500px" style="width: 100%; height: 500px; border-bottom: 1px solid #ccc;" referrerpolicy="strict-origin-when-cross-origin" frameborder="0" webkitallowfullscreen="webkitallowfullscreen" mozallowfullscreen="mozallowfullscreen" allowfullscreen="allowfullscreen" allow="camera; microphone; clipboard-write;" sandbox="allow-scripts allow-forms allow-same-origin allow-presentation allow-downloads allow-modals allow-popups allow-popups-to-escape-sandbox allow-top-navigation allow-top-navigation-by-user-activation"></iframe>

Follow the tutorial above. At this point, you have successfully created an integration! Anyone with the internal integration secret and the database ID will be able to POST content to this database, or GET content from it, using an [API request](https://developers.notion.com/reference/post-page).

For example, you could POST a new task to my Kanban template by running the following Python code:

```python
endpoint = "https://api.notion.com/v1/pages"
headers = {
    "Authorization": f"Bearer {INTERNAL_INTEGRATION_SECRET}",
    "Content-Type": "application/json",
    "Notion-Version": "2022-06-28"
}
body = {
    "parent": {
        "database_id": DATABASE_ID
    },
    "properties": {
        "Name": {
            "title": [
                {
                    "text": {
                        "content": TASK_TITLE
                    }
                }
            ]
        },
        "Status": {  # This indentation level specifies the name of the property (e.g. "Status")
            "select": {  # This indentation level specifies the type of the property (e.g. Select property)
                "name": "High priority"
            }
        }
    },
    "children": [
        {
            "object": "block",
            "paragraph": {
                "rich_text": [
                    {
                        "text": {
                            "content": TASK_CONTENT
                        }
                    }
                ]
            }
        }
    ]
}

response = requests.post(endpoint, headers=headers, data=json.dumps(body))

if response.status_code == 200:
    print("Task successfully posted to Notion!")
```

If your database is set up differently, then you might have to modify some of the `properties` to match your setup.

## Step 3: Create the iOS Shortcut

The last step is to create an iOS shortcut that sends this POST request. You can download my shortcut template [here](https://www.icloud.com/shortcuts/37b7ede5866846558e3a64277f3f6a8e). Just replace the first two text boxes with your database ID and your internal integration secret (and modify the `properties` to match your database, if necessary).

Voila! Now, when you run the shortcut, it will prompt you for a task, then add it to your database.

<img src="/assets/posts/notion-task-prompt.jpg" width="400px">

The best part: if you rename the shortcut to something like "Add A Task," then you can run this shortcut with a simple voice command by saying, **"Hey Siri, add a task."**

*Special thanks to [this guide](https://difficult-walker-d07.notion.site/Quick-add-tasks-to-Notion-0ba8167052d740878ca857080836749e) for the inspiration.*
