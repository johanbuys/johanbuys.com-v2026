---
title: "Food AI: LLM-Powered Meal Analysis (In Development)"
description: "Currently building an LLM-powered meal identification and dietary analysis feature at Cylinder Health. Members will photograph or describe a meal and get nutritional estimates, ingredient breakdowns, and GI-specific flags like FODMAP content."
pubDate: 2026-01-12
featured: true
tags: ["AI/ML", "LLM", "HealthTech", "Nutrition"]
techStack: ["TypeScript", "React Native", "Go", "Firebase", "Pub/Sub", "LLM"]
url: "https://cylinderhealth.com"
---

## Overview

Food AI is an LLM-powered feature we're currently developing at Cylinder Health. When launched, it will help members understand what they're eating and how it might affect their GI symptoms. A member takes a photo of their meal or describes it in text, and the system identifies ingredients, estimates nutritional values, and performs a dietetic analysis with GI-specific flags.

## How It Will Work

The system will accept either an image or a text description. The LLM identifies individual ingredients and estimates macronutrient and micronutrient values. It then runs a dietetic analysis that flags GI-relevant markers: high FODMAP ingredients, high fat content, excessive sodium, common trigger foods, and other factors that could aggravate digestive symptoms.

When the model isn't confident about an ingredient or portion size, it asks the member clarifying questions to improve accuracy. This conversational approach makes the results more reliable without requiring members to manually log every detail.

## Evaluation System

Like our Stool Scan feature, Food AI will be connected to a custom evaluation system. Our team of Registered Dietitians will review model outputs and provide structured feedback on accuracy, missed ingredients, and flagging quality. This feedback loop will drive continuous improvement in both identification accuracy and the relevance of dietary recommendations.

## Why We're Building This

For many GI conditions, diet is the primary lever for symptom management. Members need visibility into their dietary patterns to identify potential triggers, and our care team needs that data to guide treatment between appointments. Food AI will close that gap by making meal tracking simple, accurate, and clinically useful.
