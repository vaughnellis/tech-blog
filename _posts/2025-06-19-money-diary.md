---
layout: post
permalink: "/post/software-engineering/money-diary-v1"
title:  "Money Diary v1.0"
categories: [Personal Finance, Software Engineering]
tags: [React, Azure, Cosmos DB, Personal Finance, Budgeting, Cross-Platform]
---

Hey there, it's been a while!

I've posted a blog about WORA and this app would be the first use case.

Join me as I walk you through the app!

Setting up of expectations, I will be going through the agenda below:
1. App Background
2. Features and Gaps
    - Financial Wellbeing Questionnaire
    - Dashboard
    - Settings
    - Income Awareness
    - Category-Based Budgeting
    - Automation & Sync (Bank Allocation + Bank Discrepancy)
    - Money Goal
3. Tech Stack and Design
4. Roadmap

Let's get to it!


## App Background

# Money Diary

I named this app *Money Diary* because majority of the feature has been derived from the book **The Money Diary: End Your Money Worries NOW and Take Control of Your Financial Future** which was written by **Jessica Irvine**

From the name, perhaps you got some idea what it's all about. 
This app is designed to help take control of your finances, one mindful moment at a time.

These are principles that has been derived from the book:
1. Know Thy Money (Self-Awareness & Emotional Check-Ins)
- This encourages us to reflect on our emotional and situational relationship with money.
2. Assign Every Dollar a Job (Zero-Based Budgeting/Planning)
- Jess advocates giving every dollar a role — even fun money — to prevent leakage and anxiety.
3. Categorical Budgeting Anchored in Values
- Personalize our budget and include categories that matter to us emotionally and practically (e.g. guilt-free spending, long-term goals).
4. Track Income and Automate Goals
- Clear and visualized income sources reflect her strategy to understand all streams, no matter how small, and direct them with intent.
5. Embrace Imperfection (Don’t Overthink It)
- Consistent with her voice throughout the book — progress over perfection. She urges us to get moving, not get stuck in analysis.
6. Savings as a Future Fund
- Jess uses the term *Future You* frequently, which encourages emotional savings motivation.


What I brought in from a combination of things that I find would work for me:
1. Bank Allocation Matching
- This supplements the zero-based budgeting/planning where we also give a specific bank account a single responsibility (e.g. Commbank Savings = Bills, NAB Savings = Lifestyle expenses, etc.)
2. Bank Discrepancy Tracking
- This feature bridges the gap of instances where we tend to miss out on tracking. The app can easily identify the discrepancy based on the amount tracked versus what is currently reflecting in your actual bank account.
3. Dynamic Period-Based Budgeting
- This allows us to plan ahead so we can have a forecasted view of the total expenditure for the months to come.
- Jess encourages a month-to-month reviews so we're kind of getting ahead here.
4. Money Goal
- While Jess encourages financial goal-setting (e.g. save $1,000 emergency buffer, pay off debt, etc), she doesn't frame it as a trackable goal.
- We are taking this principle further and see the progression of the goal we set!

## Features

*Note*: *Since this is the first use case that uses the WORA template, I have not designed this for each specific platform yet. :)*

# Financial Wellbeing Questionnaire

Jess begins the book by emphasizing mindset and self-awareness before behavior change. <br/>
So.. I made it a splash screen!

#### Mobile

![Money Diary](/assets/moneydiary-f1-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f1-web.gif)

#### Desktop


![Money Diary](/assets/moneydiary-f1-desktop.gif)


# Room for Improvement

More around the UI/UX:
1. Adding a "Not Sure / Prefer  not to say" option
2. Perhaps adding emotional visual
3. Extending the score with a summary, emotional cue phrase. (not just 'Having trouble', 'Getting by', 'Just Coping', 'Doing great')

__________________

# Dashboard

Let's pretend in an alternate universe that I am a **badass executive chef** and based on google search, the salary ranges from $110,000 to $130,000. And can also exceed $150,000. <br/> For this exercise, I'll just use $130,000.

<img src="/assets/moneydiary5.png" alt="MoneyDiary">

<br/>

*Note: I am already using this app personally and what I will show you is my dev environment which I have cleaned up (data wise).*   <br/>
*Update: Sorry, I lie. I missed one test data in the Savings category and didn't want to redo the screen recording lol*

#### Mobile

![Money Diary](/assets/moneydiary-f2-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f2-web.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f2-desktop.gif)

# Room for Improvement

Lots to improve!

1. I want to see statistics/metrics/visualization based on all the data (Progress towards monthly goal, debt, overspend, trends/patterns, etc).
2. I want to add an emotional touch where I can set an emoji or mood icon per category.
3. List goes on..

__________________

# Settings 

This is the planning stage where I dictate the allocation of my income. 
<br/> We will see this reflect in the *Planned* amount in the Dashboard.

#### Mobile

![Money Diary](/assets/moneydiary-f3-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f3-mobile.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f3-desktop.gif)

# Room for Improvement

So much stuff to improve on!
Once we go through the other features, we’ll see that the majority are still static—and the objective is to make the app so flexible that whatever preference the user has can be accommodated.

__________________


# Income Awareness 

This is where we set how big our shovel is. (That phrase comes from *Dave Ramsey*)
Quick recap, as a badass executive chef, I am earning $130,000 and we need to take out the tax and super.
Based on this paycalculator tool, the monthly takeaway pay/net income would be $8,129.

<img src="/assets/moneydiary6.png" alt="MoneyDiary">


*Note: Remember, we set our settings (planned allocation). Once we apply our primary and/or secondary income, it should now reflect in the planned amount.*

#### Mobile

![Money Diary](/assets/moneydiary-f4-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f4-web.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f4-desktop.gif)

# Room for Improvement

Make the income flexible where I can add more. (It's currently static with the primary and secondary) <br/>
By day I work as a badass executive chef and by night, I can work as a bartender!

During the weekend, I can do some catering work.

The sky is the limit!


__________________


# Category-Based Budgeting 

This is where Jess advocates giving every dollar a role! (Even fun money)

For now, you can watch me while I painfully map all of my expenses. <br/>
I'll split the data entry to other platform. <br/>
Mobile will cover Bills while Web will cover Future Fund then the Desktop will cover the rest.

#### Mobile

If you're wondering, the format of this feature is always Mobile > Web > Desktop.  <br/> 
This is because I use this app personally in my phone and I just use the web/desktop when I build & test.

![Money Diary](/assets/moneydiary-f5-bills-mobile.gif)

#### Web

This covers the Future Fund category. 

![Money Diary](/assets/moneydiary-f5-future fund-desktop.gif)

#### Desktop

This covers the Savings, Investment, and Healthcare category.
 
![Money Diary](/assets/moneydiary-f5-future fund-web.gif)


### Lifestyle

This is where the main tracking sits as the other categories are mostly static/recurring. 
I've added a micro-tracking feature based on the plan to understand where the money should go to (Eating out, Hobbies, Miscellaneous, and Essentials) 

![Money Diary](/assets/moneydiary-f5-lifestyle-mobile.gif)

# Room for Improvement

Lots of things to improve!
This feature currently lacks emotional context, which is the heart and soul of the app (Financial Wellbeing).

Anyway, this is just the early stage, and I’ve also added a roadmap section based on my interpretation of Jess’s book.


__________________


# Automation & Sync

Knowing where your money should be is one thing—knowing where it actually is, is another.

This feature bridges the gap between your planned budget and your real bank activity. By comparing your expected allocations with your actual bank balances, you’ll spot mismatches, catch overspending early, and stay accountable without guesswork.

It’s financial awareness, powered by automation—so you can focus less on reconciling, and more on refining your habits.

#### Bank Allocation

I try to follow *single responsibility principle* with my bank accounts to keep things simpler and more organized.

Before my pay comes in, I want to have a clear view of where the money should go (which bank account).


#### Mobile

![Money Diary](/assets/moneydiary-f6-bankalloc-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f6-bankalloc-web.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f6-bankalloc-desktop.gif)

#### Bank Discrepancy

Sometimes I forget to track expenses, which leads to discrepancies.
This feature quickly helps identify any gaps in the recorded amounts.
It usually means either money has come in or some data entries are missing.

#### Mobile

![Money Diary](/assets/moneydiary-f7-bankdisc-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f7-bankdisc-web.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f7-bankdisc-desktop.gif)

__________________

# Money Goal

#### Mobile

![Money Diary](/assets/moneydiary-f8-moneygoal-mobile.gif)

#### Web

![Money Diary](/assets/moneydiary-f8-moneygoal-web.gif)

#### Desktop

![Money Diary](/assets/moneydiary-f8-moneygoal-desktop.gif)


## Tech Stack & Design


My objective from the start of build was to create the tracer bullet of the app. 
I just wanted to see if the concept works for me before I decide if I want to move forward.

So.. I decided to follow a frontend-driven architecture, where the business logic and state management are handled entirely in the React frontend using Redux Toolkit.
The backend will be impleneted using a serverless, function-based approach that just expose lightweight HTTP endpoints that follow a Backend-for-Frontend pattern.
This design enables me for fast iteration and full control of the UX from the frontend.

Now, as mentioned, this app is my first use case that use the WORA template that I published. <br/>
You can find it <a href="https://vaughnelliseramos.com/post/software-engineering/WORA">here</a>.

Let's break it down further.

### Frontend

Library | Role | Purpose 
React | Core UI Framework | Component-based rendering
Electron | Desktop wrapper | Converts the web app into a cross-platform desktop app
Cordova | Mobile wrapper | Wraps the React build into a native mobile shell
CRACO | Build override | Custom Webpack tweaks without ejecting CRA
Redux Toolkit + React Redux | State store | Centralised state management
Axios | API client | Talks to backend
MUI | Component library & styling engine | Rapid, themeable UI
Bootstrap 5 + React-Bootstrap | Secondary styling component set | Lightweight grid & utility classes
FontAwesome + React-Icons | Icon sets | Semantic icons without custom SVG work
Chart.js + react-chartjs-2 | Chart library | Analytics chart
React-Swipeable | Gesture helper | Smooth mobile swipes for date-range navigation
React-Toastify  | Notifications  | Toasts for success or error
React-Spinners | Loaders | Spinners for API waits
Moment.js | Date utilities | Handles period maths & formatting
@fontsource/inter | Font package | Ensure consistent typography offline


### Backend

I decided to go with Azure Logic Apps since I already had so much history with the tech.
The data store of choice initially was MongoDB.

Before I commit, I had to do a feasibility check first by building a PoC.
The PoC would have write and read operations that integrates MongoDB.

So.. I provisioned a MongoDB Cluster and read up what's required from a connector perspective which can be found <a href="https://learn.microsoft.com/en-us/connectors/mongodb/">here</a>. <br/>
It states that the pre-req for integration was to create a Data API key in MongoDB. 

After looking into it, I found this <a href="https://www.mongodb.com/docs/atlas/app-services/data-api/#1.-enable-the-data-api">document</a>. 
It indicates that the Atlas Data API has been deprecated which is a big constraint for me.

Going back to the design, I wanted to build a backend that's lightweight and I did not want to supplement this constraint by introducing a function app just to write and read to MongoDB.

This is where I decided to go with Azure Cosmos DB.

Let's dig a bit deeper:

To reiterate, we don't need to over engineer for now as a tracer bullet is intended to be just the skeleton. <br/>
Basically ensuring that it works! 

What I need is just 4 lightweight workflows:

    1. Create or update operation

<img src="/assets/moneydiary1.png" alt="MoneyDiary">

    2. Delete operation

<img src="/assets/moneydiary2.png" alt="MoneyDiary">

    3. List All Transaction operation

<img src="/assets/moneydiary3.png" alt="MoneyDiary">

    4. List by Tag operation

<img src="/assets/moneydiary4.png" alt="MoneyDiary">


From the data store side, the initial design I had in mind was to isolate the data from a container level.
Going back to the features, since we have the category-based budgeting, the plan was to have one for each (Bills, Lifestyle, Savings, Future Fund, etc.)

I then realize that perspective was coming from a SQL design and not of a schema-flexible mindset. <br/>
I decided to just have one container that basically acts as a *ledger* and that the main focus of the design would be on the payload.


Below is the current document design I have:

#### Income Awareness
```json
{
    "id": "income-master",
    "type": "income",
    "monthlyIncome": 8129,
    "secondaryIncome": 2000,
    "userId": "master",
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```

### Secondary Income
This can be allocated/split into different bank accounts.

```json
{
    "id": "secondary-income-allocation-master-2025-07-14",
    "type": "secondary-income-allocation",
    "allocations": [
        {
            "amount": 2000,
            "bank": "Commbank",
            "bankAccount": "Savings",
            "tag": "Savings"
        }
    ],
    "allocationDate": "2025-07-14",
    "userId": "master",
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```

###  Category-Based Budgeting
```json
{
    "id": "123456789",
    "name": "Rent",
    "amount": 2600,
    "category": "Essentials",
    "subCategory": "Rent",
    "date": "6/26/2025",
    "merchant": "Abbotsford NSW",
    "bank": "Commbank",
    "bankAccount": "Transaction",
    "comments": "This should calculate all rent for the entire cutoff period.",
    "type": "expense",
    "account": "nab-vaughn",
    "userId": "master",
    "tag": "Bills",
    "_weeklyRate": 650,
    "isRecurring": true,
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```

### Money Goal
```json
{
    "id": "123456789",
    "type": "money-goal",
    "goalTitle": "Emergency Fund",
    "goalAmount": 5000,
    "targetDate": "2026-07-12T12:39:50.255Z",
    "monthsToGoal": 12.8,
    "daysToGoal": 384,
    "userId": "master",
    "monthlySetAside": 391.633,
    "goalBank": "Commbank",
    "goalBankAccount": "Savings",
    "saved": 0,
    "isCompleted": false,
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```

### Lifestyle Settings
```json
{
    "id": "lifestyle-settings-master",
    "type": "lifestyle-settings",
    "data": [
        {
            "name": "Eating Out",
            "percentage": 40
        },
        {
            "name": "Essentials",
            "percentage": 10
        },
        {
            "name": "Hobbies",
            "percentage": 30
        },
        {
            "name": "Miscellaneous",
            "percentage": 20
        }
    ],
    "userId": "master",
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```

#### Settings

```json
{
    "id": "123456789",
    "type": "settings",
    "data": [
        {
            "name": "Miscellaneous",
            "percentage": 0
        },
        {
            "name": "Investment",
            "percentage": 5
        },
        {
            "name": "Savings",
            "percentage": 29.745285813012142
        },
        {
            "name": "Future Fund",
            "percentage": 10
        },
        {
            "name": "Expense",
            "percentage": 0
        },
        {
            "name": "Food Expense",
            "percentage": 0
        },
        {
            "name": "Bills",
            "percentage": 60
        },
        {
            "name": "Lifestyle",
            "percentage": 9.435354902201992
        },
        {
            "name": "Healthcare",
            "percentage": 5
        }
    ],
    "userId": "master",
    "_rid": "secret",
    "_self": "secret",
    "_etag": "secret",
    "_attachments": "attachments/",
    "_ts": 123456789
}
```


## Roadmap

This app definitely does not give a *diary* feels yet and has not applied the principles that is being taught by Jess.

Below is the list of features that I want to bring in which is categorized by priority:

Principle | Explanation | Goal | Tools | App Feature
Daily Money Diary | Track daily spending, how you felt, and why | Build habit & self-awareness | Journaling and check-ins | Daily Journal with spend, emotion, and notes
Mindful Spending / Emotional Awareness | Understand the *why* behind the money behavior | Spend intentionally and reduce guilt | Reflection prompts | Pre-spend prompts with goal and mood alignment
Impulse Triggers | Recognize emotional drivers of spending | Reduce unconscious and emotion-driven spending | Mood tags and trigger logs | Introduce a *trigger* selector with trend analysis
Month-to-Month Reviews | Reflect monthly on what worked or didn't | Improve decision-making over time | Journaling and review cards | Monthly pop-up summary and reflection prompt
Stages of Change (Behavior Model) | Know where you are on the behavior change spectrum | Personalize advice | Quiz and milestone mapping | Behavior stage tracker with tailored messages
4 Pillars of Financial Wellbeing | Control, Buffer, Goals, Confidence | Track holistic money health | Pillar tracker and radar chart | Improve Dashboard metrics and add visual tracker for each pillar with tailer guidance
Money Types / Financial Identity | Know if you're a spender, avoider, etc | Build tailored strategies | Personality quiz | Introduce quiz/questionnaire with dynamic dashboard tips per type
Money Mind Map | Map your values, fears, goals visually | Deepen emotional money connection | Visual Map | Interactive mind map linking money beliefs and behavior
Behavioral Nudges | Subtle prompts to improve outcomes without forcing | Encourage better decisions | Smart popups and reminders | Nudge system triggered by spending patterns
Celebrate Small Wins | Recognition to build positive reinforcement | Create motivation & habit loop | Badges, toasts, and streaks | Rewards system for habit milestones
Annual Review | Review the full year's financial journey | Celebrate growth and identify gaps | Timeline/PDF report | Year-in-review dashboard or exportable pdf summary
Net Worth Tracking | Assets - Debts = True financial picture | Understand long-term growth | Asset/debt entry and metrics | Add net worth menu/tab with time-series metrics


This framework was introduced by **Dave Ramsey** and I would also like to see **Debt Snowball Tracker** feature.
This feature aims to pay smallest debts first to build momentum.


Thanks for joining me as I document my journey! :)