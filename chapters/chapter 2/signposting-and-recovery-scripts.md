# Signposting Phrases & Recovery Scripts

Ready-to-use language for driving an AI system design interview and getting unstuck. Practice these out loud in mock interviews until they feel natural — the interviewer can only evaluate reasoning they can hear.

---

## 1. Opening & scoping (Phase C)
- "Before I design anything, let me clarify the requirements so I solve the right problem."
- "I'd like to understand four things: the product context, the scale, the constraints, and how we measure success."
- "What surfaces are we designing for, and what's the latency budget?"
- "How many daily active users should I design for, and what's the peak QPS?"
- "Let me write these down as a quick requirements doc so we can refer back to them."

## 2. Stating assumptions (use throughout, especially when the interviewer deflects)
- "For the scope of this interview, I'll focus on [X] and assume [Y]. Flag me if that's not what you had in mind."
- "I'll assume 100M DAU and a p99 latency under 100 ms. If that's different, we can adjust."
- "Since the scale isn't specified, I'll design for 10M users initially with a clear path to 100M — that affects our database and caching choices."
- "There are a few ways to frame this ML problem; I'll frame it as retrieval + ranking. We could also do end-to-end generation if latency allows."

## 3. Signposting / transitions (guide the interviewer's rubric)
- "Let me start by clarifying the requirements."
- "I'll structure the design in three parts: data, training, and serving."
- "Now moving to the serving layer…"
- "Before I go deeper, does this high-level flow make sense?"
- "To summarize what we've discussed so far…"
- "That covers the training pipeline — I'll move to the serving layer next, then we can drill into whichever you prefer."
- *(Meta-style)* "Let me now cover the data and labeling strategy, then features, then the model."

## 4. Driving the conversation (without steamrolling)
- "I've covered the training pipeline. Let's discuss the serving layer next, before diving deeper."
- "There are two areas we could go deep on — the feature store or the ranking model. Which is more useful to you?"
- "I'll give a quick pass across all components for breadth, then go deep where you'd like."
- *(Follow their cue immediately)* "Sure — let me switch to the feature store since you'd like more there."

## 5. Signaling depth (the T-shape)
- "I have a lot of experience with feature stores; I can go deeper there if useful."
- "The serving layer is critical here — let me spend a bit more time on that."
- "Would you like me to elaborate on the training pipeline? That's where I've done most of my recent work."

## 6. Inviting feedback & collaborating
- "Does this direction align with what you had in mind?"
- "Is there an area you'd like me to focus on?"
- "Have you seen a different approach that worked well in your experience?"
- "That's a good point — we could add a cache there to reduce latency." *(acknowledge suggestions)*
- *(Reading cues)* If they look confused, pause and clarify; if they nod quickly, move on.

## 7. Recovery scripts — when you're stuck
Interviewers don't expect you to know every domain; they score your **approach**. Use these in order:

1. **Pause & acknowledge**
   - "I'm not immediately sure about the best approach here. Let me think through the options for a moment."
2. **Break it down**
   - "This seems to have two parts — retrieval and ranking. Let me tackle retrieval first."
   - "Let me reduce this to a smaller sub-problem I'm confident about, then build back up."
3. **Ask for a nudge**
   - "Is there a particular direction you'd like me to explore?"
4. **Propose & iterate** *(preferred for senior roles)*
   - "One approach could be X. Would that work, or do you see issues?"
   - "I'll commit to approach X for now and revisit if we hit a constraint."

## 8. Recovering from a wrong turn
- "Let me step back — that approach adds complexity without buying us much. I'll take a cleaner path."
- "On reflection, my earlier assumption about [X] doesn't hold. Here's how that changes the design."
- *(Correcting course gracefully often scores better than a lucky flawless run.)*

## 9. Turning ambiguity into an opportunity (senior signal)
- "We don't know the cold-start requirements, so I'll design for both new users and new items and prioritize based on product focus."
- "The problem is underspecified, which is fine — framing it well is part of the job. Here's the framing I'll commit to and why."

## 10. Closing (Phase E)
- "To wrap up: here's the end-to-end design, the two trade-offs I'd highlight, and what I'd improve next."
- "If I had more time, I'd deepen [X], add [responsible-AI guardrail], and optimize cost via [caching/model routing]."
- "Alternatives I considered but rejected: [A] because [reason]."

---

> **Practice tip:** Pick 2–3 phrases from each section and rehearse them in every mock until they're automatic. Signposting and calm recovery are learned behaviors, not talents.
