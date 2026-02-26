---
title: "Engineering Manager's Toolkit"
description: "A set of LLM-powered Claude Code Skills that helps engineering managers lead teams at scale. Connects with GitHub, Jira, and Slack to surface actionable insights into team flow, velocity, code quality, and individual growth opportunities."
pubDate: 2026-02-23
featured: true
tags: ["AI/ML", "Engineering Management", "Developer Tooling", "Side Project"]
techStack: ["TypeScript", "Claude Code Skills", "GitHub API", "Jira API", "Slack API"]
---

## Overview

Engineering Manager's Toolkit is a set of Claude Code Skills I'm building to solve a problem I deal with every day: staying on top of everything happening across a growing engineering team without burning all my time on manual data gathering.

It connects to GitHub, Jira, and Slack to pull together information about PRs, tickets, conversations, and code changes, then uses LLMs to surface actionable insights about team flow, velocity, and individual engineer performance.

## What It Does

**Team Flow and Velocity.** The toolkit ingests PR data, ticket movement, and communication patterns to build a picture of how work is actually flowing through the team. It flags bottlenecks, stalled PRs, and patterns that suggest process friction before they become problems.

**PR Review Insights.** It reviews pull requests and extracts signals about code quality, test coverage patterns, and common review feedback themes. Over time this builds a picture of where the team is strong and where there are gaps.

**Engineer Profiles.** For each team member, the toolkit builds a profile based on their PR activity, ticket history, and code review patterns. This isn't about surveillance. It's about having real data when I walk into a 1:1, so I can give specific, actionable feedback instead of vague impressions.

**1:1 Meeting Support.** It ingests transcripts from 1:1 meetings, extracts action items, generates summaries, and feeds everything into a knowledge base. When performance review season comes around, I have months of context organized and searchable instead of scrambling to remember what we talked about in March.

## The Growth Framework

At the core of the toolkit is a framework I developed for identifying growth opportunities. It looks at patterns across an engineer's work (the types of PRs they submit, the complexity of tickets they pick up, the feedback they give and receive in reviews) and surfaces coaching opportunities. For example, it might flag that an engineer has been doing great on feature work but hasn't taken on any infrastructure tasks, or that their PR review comments are consistently surface-level, suggesting an opportunity to mentor them on deeper code review.

## Why I'm Building This

Managing a team well requires a lot of context, and most of that context lives scattered across five different tools. I spend too much time clicking through Jira boards, scrolling Slack threads, and reviewing GitHub activity just to build a mental model of what's going on. The toolkit automates the gathering and synthesis so I can spend that time on what actually matters: coaching, unblocking, and helping my team grow.
