---
title: "Stool Scan: AI-Powered Stool Assessment"
description: "Built an AI-powered stool assessment feature at Cylinder Health. Members photograph a sample, and a custom-trained, clinically validated model analyzes it to produce a Bristol Stool Score and other diagnostic factors for the clinical team."
pubDate: 2026-02-12
featured: true
tags: ["AI/ML", "HealthTech", "Computer Vision", "Clinical"]
techStack: ["TypeScript", "React Native", "Go", "Firebase", "Pub/Sub", "Custom ML Model"]
url: "https://cylinderhealth.com"
---

## Overview

Stool Scan is an AI-powered feature at Cylinder Health that lets members photograph a stool sample for instant clinical analysis. A custom-trained, clinically validated model analyzes the image and returns a Bristol Stool Score along with other diagnostic factors. The results feed directly into the clinical workflow, giving our care team objective data to assist in patient care.

## How It Works

A member opens the Cylinder app, takes an image, and submits it. The image is processed through our custom ML model, which was trained and clinically validated in partnership with GI researchers. The model returns a Bristol Stool Score and flags relevant clinical markers. Our clinical team uses these results alongside other member data to guide treatment decisions.

## Continuous Improvement

The system is hooked into a custom evaluation pipeline where our team of Registered Dietitians reviews model outputs and provides structured feedback. This human-in-the-loop approach lets us continuously improve accuracy and catch edge cases that pure automated metrics would miss. The RD feedback flows back into model training and prompt refinement cycles.

## Why It Matters

GI conditions are notoriously hard to track objectively. Patient-reported outcomes are inconsistent and often inaccurate. By giving members a simple way to capture objective data, we reduce the burden on patients while giving clinicians better information to work with. Cylinder acquired Dieta Health's stool imaging AI technology to build on peer-reviewed clinical research from institutions like Cedars-Sinai and Mayo Clinic.
