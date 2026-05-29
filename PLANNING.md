# StreakUp – Career Accountability Platform

## Project Overview

StreakUp is a 75-day career accountability platform for anyone 
actively job searching. Users set daily goals based on their 
career track, log progress every day, earn points and badges 
for consistency, and get AI coaching on what to focus on next.

The core rule: show up every day or restart from Day 1.

Live demo: (coming soon)
GitHub: https://github.com/s-r-a-v-y-a/streak-up

---

## Problem it solves

Job searching is lonely, inconsistent, and hard to measure. 
Most people apply for a few days then lose momentum. StreakUp 
gamifies the process by turning 75 days of consistent effort 
into something trackable, rewarding, and social.

---

## Target users

- Software engineers job searching
- Business analysts job searching
- Designers, product managers, marketers job searching
- Anyone who wants a structured 75-day career sprint

---

## Core rules

1. When you register, Day 1 starts today automatically
2. You must log activity every day to maintain your streak
3. Miss one day = streak resets to 0, back to Day 1
4. Grace period option: users can choose 1 grace day per week
5. Your public profile shows streak and badges only
   Your tasks, targets, and logs are always private

---

## Features

### Onboarding
- Pick career track (Software Engineer, Business Analyst, 
  Product Manager, UI/UX Designer, Marketing, Finance, Other)
- See suggested daily tasks for your track
- Customize tasks: add, remove, edit
- Set daily targets per task
- Choose strict mode or grace period mode

### Career track suggestions

Software Engineer:
- Job applications (number, target: 20)
- Coding problems / LeetCode (number, target: 2)
- GitHub commit (yes/no)
- LinkedIn activity (yes/no)
- Course / learning (minutes, target: 30)
- Project work (yes/no)

Business Analyst:
- Job applications (number, target: 20)
- SQL practice (yes/no)
- Excel or Tableau practice (yes/no)
- LinkedIn activity (yes/no)
- Course / learning (minutes, target: 30)
- Case study practice (yes/no)

Product Manager:
- Job applications (number, target: 20)
- Product case study (yes/no)
- LinkedIn activity (yes/no)
- Course / learning (minutes, target: 30)
- Reading articles or books (yes/no)
- Portfolio work (yes/no)

UI/UX Designer:
- Job applications (number, target: 20)
- Figma or design practice (yes/no)
- Portfolio piece progress (yes/no)
- LinkedIn activity (yes/no)
- Course / learning (minutes, target: 30)
- Dribbble or Behance post (yes/no)

### Daily logging
- See today's tasks with progress bars
- Check off completed tasks
- Enter numbers where relevant
- Real-time motivational messages based on progress
- Points earned as you log
- Celebration on perfect day
- Add a daily note

### Motivational messages
Below 50% of target:
"You are just getting started. Keep going!"

At 80% of target:
"So close! Just a little more and you hit your goal."

At 100% of target:
"Target hit! You showed up today and that matters."

Exceeded target:
"You crushed it! Bonus points earned!"

Streak broken:
"Your streak ended. That is okay. 
Start fresh tomorrow — your best streak is ahead."

### Points system
Meet daily target per task:     1 point
Exceed daily target per task:   2 points
Complete ALL tasks in a day:    5 bonus points (perfect day)
7-day streak:                   10 bonus points
30-day streak:                  50 bonus points

### Badges and milestones
10 points   → Bronze  "Getting Started"
25 points   → Silver  "Building Momentum"
50 points   → Gold    "Unstoppable"
100 points  → Platinum "Career Champion"
200 points  → Legend  "The 75-Day Warrior"

Users set their own reward for each milestone during onboarding.

### Progress dashboard
- Current streak and longest streak ever
- Total points
- Day number (Day X of 75)
- Charts per task over time
- Weekly report every Sunday

### AI Coach (Gemini API - free tier)
- Analyzes last 7 days of activity
- Daily personalized suggestion
- Weekly summary every Sunday
- Streak break motivation
- Career track specific tips

### Friends and groups
- Create a group with invite code
- See friends streaks and points on leaderboard
- Cheer someone on (reaction button on their day)
- Group is private — only members can see each other

### Public profile
Shows publicly:
- Name
- Career track
- Current streak
- Longest streak
- Total points
- Badges earned
- Day number (X of 75)

Always private:
- Daily task list
- Targets
- Daily logs and notes
- Charts and detailed analytics

### Landing page
- Hero section: what is StreakUp
- How it works (3 steps)
- Career tracks section
- Points and badges preview
- Testimonials (add after launch)
- Sign up call to action

---

## Tech stack

Frontend:   Next.js, React, Tailwind CSS, Framer Motion
Backend:    Node.js, Express.js
Database:   Neon.tech (free PostgreSQL)
AI:         Google Gemini API (free tier - 1500 calls/day)
Auth:       JWT, bcrypt
Deployment: Vercel (frontend), Render (backend)

---

## Database schema

User
- id, name, email, password
- careerTrack
- gracePeriodEnabled (boolean)
- graceUsedThisWeek (boolean)
- currentStreak
- longestStreak
- totalPoints
- dayNumber (1-75, resets if streak breaks)
- lastLogDate
- createdAt

Task
- id, userId
- name, icon
- type (number / boolean / duration)
- dailyTarget
- unit (jobs / problems / minutes / modules)
- isActive

DayLog
- id, userId
- date, dayNumber
- totalPointsEarned
- isPerfectDay (boolean)
- note
- aiSuggestion
- createdAt

TaskLog
- id, dayLogId, taskId
- targetValue, actualValue
- pointsEarned
- status (not_started / below / met / exceeded)

Badge
- id, userId
- badgeName, badgeLevel
- earnedAt
- userReward (what they promised themselves)

Group
- id, name, createdBy
- inviteCode

GroupMember
- id, groupId, userId, joinedAt

Cheer
- id, fromUserId, toDayLogId
- emoji, createdAt

---

## Pages

/                     Landing page
/register             Sign up
/login                Login
/onboarding           Pick track, customize tasks, set targets
/dashboard            Today overview, streak, quick log
/log                  Full daily log form
/progress             Charts, streak history
/ai-coach             AI suggestions and weekly summary
/goals                Weekly targets
/friends              Group and leaderboard
/profile/:username    Public profile page
/settings             Edit tasks and targets

---

## Build phases

Phase 1 - Foundation
  Auth (register, login)
  Onboarding (career track, task setup)
  Basic daily log
  Streak tracking logic
  Day counter (auto start, auto reset)

Phase 2 - Gamification
  Points system
  Badge awarding
  Progress bars
  Motivational messages
  Perfect day celebration animation

Phase 3 - Dashboard and Charts
  Progress charts per task
  Streak history
  Weekly report

Phase 4 - AI Coach
  Gemini API integration
  Daily suggestions
  Weekly summaries
  Streak break messages

Phase 5 - Friends and Groups
  Group creation with invite code
  Leaderboard
  Cheering system

Phase 6 - Landing Page and Polish
  Landing page
  Public profiles
  Mobile optimization
  Deploy to Vercel and Render