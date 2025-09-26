---
layout: post
permalink: "/post/software-engineering/money-diary-v1"
title:  "Money Diary v2.0"
categories: [Personal Finance, Software Engineering]
tags: [React, Electron, Cordova, Capacitor, Azure, Logic Apps, Cosmos DB, Personal Finance, Budgeting, Cross-Platform]
article-series:
  id: "money-diary-series"
  series-title: "Money Diary"
  sidebar-label: "V2.0"
  part: 2
  total: 2
---

Hey there, It's been a while since my first post about my passion project and both excited and slightly overwhelmed by how much this project has progressed. 

I wanted to try something new this time and make this simple.

## Agenda:
1. What's New
2. What's Cookin'
3. What's Next

## What's New:

#### Look and Feel
1. **Updated navigation to hamburger menu**
![Money Diary](/assets/md-v2-nav-01.gif)
This makes it much more easier to navigate between features.

#### Financial Management
1. **Added Multiple Income Stream**
![Money Diary](/assets/md-v2-income-02.gif)
This enables you to consolidate all of your income streams and take control of them!

2. **Enhanced Money Goals Planner feature**
  - Creating a Goal
  ![Money Diary](/assets/md-v2-goal-03.gif)
  Set it up, stick with it, and finally win!

  - Creating a Debt
  ![Money Diary](/assets/md-v2-debt-04.gif)
  Time to face those credit card bills or other loans! 

3. Enhanced Bank Allocation feature
![Money Diary](/assets/md-v2-bankallocation-06.gif)
Gives you a single view of where your money should sit!

4. Added Lifestyle Statistics and Dynamic Categories setting
![Money Diary](/assets/md-v2-lifestyle-statistics-07.gif)
Shows you exactly where your money goes

#### Planning & Tracking
1. Enhanced Money Goals Dashboard
![Money Diary](/assets/md-v2-goaldashboard-05.gif)
See your progress without wanting to cry.

2. Added Monthly Summary
![Money Diary](/assets/md-v2-monthly-summary-08.gif)
Your monthly "how did I spend that much?" recap.

3. Enhanced Bank Discrepancy
![Money Diary](/assets/md-v2-bank-discrepancy-09.gif)
For when you and your bank can't agree on math.

4. Added Habit Calendar
![Money Diary](/assets/md-v2-Habit-Calendar-10.gif)
Track those good general & money habits you're totally gonna stick to this time.

#### Personal Development
1. Added Monthly Intentions
![Money Diary](/assets/md-v2-intentions-11.gif)
Like New Year's resolutions but monthly and more realistic.

2. Added Monthly Reflections & Money Mindmap Check-in
![Money Diary](/assets/md-v2-reflections-12.gif)
Sometimes you gotta have a heart-to-heart with your wallet.

3. Added Monthly Checklist 
![Money Diary](/assets/md-v2-checklist-13.gif)
Who doesn't love checking stuff off a list?

4. Added Achievements feature
![Money Diary](/assets/md-v2-achievements-14.gif)
Finally, your money wins get the recognition they deserve.

5. Added Money Snapshot
![Money Diary](/assets/md-v2-snapshot-15.gif)
Quick peek at where you stand financially.

#### General Update
1. Added Initial Tooltip feature
![Money Diary](/assets/md-v2-tooltip-16.gif)
No more clicking random buttons to figure out what they do.

2. Automation of calculations (e.g. Rent / Recurring expenses for future funds)
![Money Diary](/assets/md-v2-automation-17.gif)
App does the tedious number-crunching so you don't have to.

3. Lots of bug fixes! 😅

## What’s cookin’

I started this passion project with the though process of building an MVP.
The objective was to see if this would help me and in the hopes of helping others as well.

Now that I have added a bunch of features, it has been challenging for me to manage since I have designed this as a ***thin backend*** with a ***smart client***.

To summarize:

I have the ff:
- React/Electron/Cordova/Capacitor doing **ALL** the heavy lifting on the frontend
- Azure Logic app basically just playing CRUD middleman
- Azure Cosmos DB storing everything
- ALL business logic living in the client 😆

This means I still have the same 4 operations and all business logic resides within the client(omg!😅)

![Money Diary](/assets/md-whats-cookin.png)

The good news? It works! The less good news? Every new feature feels like I'm playing architectural Jenga. 
Which is why I'm now in the planning stage to modernize the architecture.


## What's next

I'm about to make some big moves!

I want to try something completely different this time.
Once I've got the technical foundation sorted, I'll phone a UI/UX designer magician friend.
When everything is said and done, the scary and exciting part is having a select few perform beta testing!

The dream is to get this onto the Google Play Store and Apple store and actually help people manage their finances better.

If you have any comments/suggestion/recommendation/any feedback, please feel to reach out!