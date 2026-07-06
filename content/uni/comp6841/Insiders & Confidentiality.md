---
title: Insiders & Confidentiality
draft: false
tags:
  - cybersec
---
# Game Theory

[[Game Theory]] studies how individuals make decisions when their outcomes depend on others' choices - cooperation or competition. Examples are business, politics, social behaviour, environmental issues.

Within cyber security, it helps explain cooperation, trust, and conflict.

### Prisoner's Dilemma

Cooperation vs. self-interest

2 suspects are arrested for a crime, interrogated separately, each can cooperate (stay silent) or defect (betray the other).

Outcomes:
- both cooperate --> light sentence for both.
- one defects, other cooperates --> defector goes free, cooperator gets heavy sentence.
- both defect --> moderate sentence for both.

The conclusion is that rational self-interest puts both parties at a disadvantage.

### Cooperation

Trust, alongside repeated demonstrations of trust encourage cooperation over time as well as reputation. Incentives like legal frameworks or industry standards can promote collaboration.

Social engineering exploits human trust, turning cooperation against security.

### Tragedy of the Commons

Overuse of shared resources

Individuals share a common resource. Each acts in their own interest to maximise personal benefit. Results in resource depletion or degradation harming everyone. For example, overfishing.

This demonstrates the need for regulation, cooperation, or incentives to protect shared resources.

### The Psychology of Deception

Misdirection can be used as exploitation. Deception isn't just about what you see, it's about what you fail to notice.

Cognitive Biases shape how we think. Cognitive Vulnerabilities show where attackers can push.

| Bias                   | Vulnerability                                               |
| ---------------------- | ----------------------------------------------------------- |
| Confirmation bias      | "I believe it because I want it to be true"                 |
| Anchoring              | "The first number/message shapes my decision"               |
| Availability heuristic | "I just heard about this scam, so this one feels real/fake" |
| Attention fatigue      | "I am too tired to check carefully"                         |
| Emotional distraction  | "I am scared, excited, or rushed"                           |
| Over-trust             | "It has a logo/name I recognise"                            |

### Social Engineering

We as humans, are emotional, trusting, curious, and sometimes distracted. Social engineering involved manipulating people into revealing confidential information or performing actions they normally wouldn't. It works because attackers design attacks around normal human behaviour: trust, helpfulness, urgency, fatigue, and routine.

It's not about breaking in, it's about being let in.

### Anatomy of a Mitnick Attack

[Kevin Mitnick](https://en.wikipedia.org/wiki/Kevin_Mitnick) is an ex-hacker, who was notorious in the 90s for hacking using social engineering rather than code.

- Information gathering: Dumpster diving, tailgating, phishing.
- Pretexting: Pretending to be someone else.
- Exploiting Human Trust - convincing users to:
	- reveal passwords
	- disable security
	- run malicious tools
- Timing the Attack - during weekends, public holidays, IT downtimes.

If you are an attacker, you will attack at a time that causes the most destruction.

90s to 2026, social engineering has scaled:

| Then                 | Now                            |
| -------------------- | ------------------------------ |
| Phone pretexting     | AI-generated phishing          |
| Dumpster diving      | LinkedIn/OSINT scrapping       |
| Tailgating           | MFA fatigue attacks            |
| Fake IT support      | Fake Teams/Zoom/Slack messages |
| Manual impersonation | Deepfake voice/video           |
What public information about you could an attacker use to make a convincing scam?


### Scams Anatomy

| Stage    | Example                                 |
| -------- | --------------------------------------- |
| Hook     | "Your account is locked"                |
| Trust    | Bank logo, name, partial details        |
| Pressure | "Act within 30 minutes"                 |
| Action   | Click link/ call number/ transfer money |
| Loss     | Credentials, money, identify data       |

### Hot States

Hot states that attacker's exploit: 
- Panic ("your account is hacked!")
- Greed ("You've won!")
- Authority pressure ("Boss needs this NOW!")

These states bypass rational thinking, shorten decision-making time, increase compliance.

Defensive strategy: Pause, verify, don't react emotionally.

### Timing Attacks - Why they work?

- psychological blind spots:
	- stress, fatigue, urgency = human error
- operational weaknesses:
	- skeleton staff on holidays
	- delayed incident response over weekends

[Colonial Pipeline (2021): Attack started on Friday --> more downtime](https://www.cisa.gov/news-events/news/attack-colonial-pipeline-what-weve-learned-what-weve-done-over-past-two-years)

Timing doesn't just affect damage, it increases likelihood of success.

### Scams

#### Deepfake Voice Scam
Scenario: An employee receives a voice message that sounds like their
manager: “I am in a meeting. Please urgently pay this supplier invoice.”

#### Romance Scams and Pig Butchering
Scammers exploit emotional vulnerability on dating platforms and social media platforms. Targets are often lonely, recently divorced or widowed, and seeking deep connection. Love can cloud judgement, and scammers know it.

![[Screenshot 2026-07-06 at 18.10.12.png]]
Avoiding being scammed: pause, verify, report.

### Conflict of Interest

When personal motives conflict with professional or ethical responsibilities.

### Corruption

Using power or position for personal gain at the expense of institutional integrity. Corruption is when the duty to yourself overrides duty to the system.

Conflict of interest becomes corruption when it's acted upon dishonestly or secretly.

- [Enron (2001): Executives hid debt and inflated profits for personal bonuses.](https://en.wikipedia.org/wiki/Enron_scandal)
- [FIFA Scandal (2015): Officials took bribes to influence tournament hosting decisions.](https://en.wikipedia.org/wiki/2015_FIFA_corruption_case)
- Police Bribery Cases: Officers accepting money to ignore crimes.
- Construction Kickbacks: Officials awarding contracts in exchange for under-the-table payments.

Corruption isn't just unethical; it destabilises systems, breaks trust, and harms entire communities.

### The Role of Impartial Third Parties

In complex systems, we rely on neutral actors to enforce rules:
- auditors: review compliance, finances, security
- referees: enforce fairness in competitive settings
The ideal referee is impartial (not influenced by teams, power, or popularity). People often resent oversight, especially when outcomes feel subjective or unfair. But true integrity means calling out wrongdoing, even in your own group. 

Who audits the auditor?
- Oversight must itself be transparent and accountable. Otherwise, trust breaks down, and insider threats go unnoticed.

### Human-In-The-Loop & AI

Would having more AI replace humans create faster decisions? Greater efficiency? Less accountability?

Can AI replace humans in positions of command (military, cyber defence, emergency response)?

Does more AI = fewer insider threats?
- AI doesn't have personal grudges or financial motives. However, AI can be misconfigured, poisoned, or manipulated.

#### Controls & Considerations

__Accountability__: Who is responsible when AI makes a wrong decision?
__Bias & Transparency__: Are AI decisions explainable and fair?
__Fail-safes__: Can a human override the AI? Under what conditions?
__Ethics__: Should life-and-death or justice-related decisions ever be automated?