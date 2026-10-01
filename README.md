# Wallet Support Triage

![Status](https://img.shields.io/badge/status-in%20progress-yellow)

The design is in [PROJECT_PLAN.md](PROJECT_PLAN.md).

Python · Streamlit · SQLite · Qwen · pytest

A support triage system for a fictional digital wallet. It reads customer messages in Arabic and English, sorts them into tickets, asks for missing details, and drafts replies. Escalation and priority are decided by rules enforced in code. No reply reaches a customer without human review.

---


## Goal and users 

**Target user**: The system has two users:
- **Customers of the wallet:** send messages regarding a problem with a payment, a top-up or withdrawal, or their account.   
- **Support staff:** who review the tickets, see which are urgent, read a draft reply when a ticket is ready and approve, edit or reject it before anything reaches the customer.


**Goal**: The goal is to reduce the time the staff spend reading and sorting messages, while keeping every reply and every risky case in human hands.

---


