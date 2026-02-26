---
title: "Migrating Our Mobile CI/CD to Expo Application Services"
description: "How we moved from a fragile local build process to Expo Application Services: the infrastructure and codebase changes, the tradeoffs, and what we gained."
pubDate: "Nov 20 2024"
---

Earlier this year, I led a project to migrate our React Native mobile app's entire build and deployment pipeline to Expo Application Services (EAS). It was one of those projects that touches everything: codebase, infrastructure, developer workflow, release process. It taught me a lot about what it takes to modernize CI/CD at a growing startup.

## The Problem

Our existing build process was fragile. Builds were inconsistent across developer machines. The release process involved too many manual steps. And as the team grew, these problems compounded. Engineers were spending time fighting the build system instead of shipping features.

We needed a system that was reproducible, automated, and fast enough that developers would actually trust it.

## Why EAS

We evaluated several options, but EAS stood out for a few reasons. It's purpose-built for React Native and Expo projects. It handles the complexity of native builds (iOS and Android) in the cloud, which eliminates the "works on my machine" problem. And it integrates cleanly with our existing Expo-based codebase.

The tradeoff is vendor lock-in and cost, but for a team our size, the productivity gains far outweighed those concerns.

## The Migration

This wasn't a weekend project. It touched both the codebase and our infrastructure.

On the code side, we had to audit and update our native dependencies, ensure our Expo config was compatible with EAS Build, and restructure how we handled environment variables and build profiles for different environments (development, staging, production).

On the infrastructure side, we set up EAS Build profiles, configured our CI pipeline to trigger builds automatically, and integrated EAS Update for over-the-air updates. We also had to rethink our release process: we moved from manual App Store/Play Store submissions to automated submissions through EAS Submit.

## What We Gained

The results were immediate and significant. Build times became predictable. Developers stopped debugging build environment issues. Our release cadence increased because the friction was gone. And critically, we could now roll out over-the-air updates for JavaScript changes without going through the full app store review cycle.

The less obvious gain was confidence. When your build system is reliable, engineers ship more boldly. They're not second-guessing whether a change will break the build or cause a release delay.

## Lessons Learned

First, invest in documentation during the migration, not after. We wrote runbooks for every step of the new process, and it paid off immediately when onboarding a new team member mid-migration.

Second, don't underestimate the cultural shift. Moving to cloud builds means giving up some control. Engineers who are used to building locally need to trust the system, and that trust is earned through reliability and transparency.

Third, do it in phases. We migrated Android first, stabilized, then moved iOS. Trying to do both simultaneously would have doubled our debugging surface area.

CI/CD isn't glamorous work, but it's the foundation everything else sits on. Getting it right multiplied our team's velocity in ways that are hard to overstate.
