# Example 5: The interview gets inherited (part 2 of 2)

The assistant in this session was built by the framework in [example 4](04-assistant-build.md). This is that deliverable running in a fresh project with no access to the framework: the interview logic travels inside the deliverable itself.

A complete, unedited session. Watch the generated coach run its embedded setup interview with the same discipline it was built under (capped rounds, readiness indicators, a gate before it acts), mine concrete details out of lazy answers, adapt a draft to blunt feedback, and flip personas into a pressuring mock interviewer mid-session without losing the user's profile. Annotations in blockquotes are added for this document.

---

**User:**

> I want to prepare for a job interview. Follow your session setup protocol — understand what I'm prepping for before jumping into practice or coaching.

**Generated assistant:**

Great, let's get you ready. I need to understand what you're walking into before we start working — a few rounds of quick questions and then we'll dive in.

🔴 Discovery

To start, three things that'll shape everything else:

1. What role are you interviewing for, and at which company? If you have the job description handy, feel free to paste it — I'll pull what I need from it.
2. What's your current or most recent role, and roughly how many years of experience are you bringing?
3. Do you know when the interview is, and what format it'll be (phone screen, video panel, on-site, etc.)?

**User:**

> second job, applying for a junior data analyst role, ~1–2 years experience, nervous about tell me about yourself and salary questions, interview is next week on site

**Generated assistant:**

Good — that's a solid start. You've already named the two areas that trip up the most candidates at your level, so we'll make sure those feel locked in before interview day.

🟡 Refining

A few more things so I can tailor this properly:

1. What's your current (or most recent) role and what tools/skills do you work with day to day? Think things like SQL, Excel, Python, Tableau, specific types of analysis — whatever you actually spend time on.
2. Which company is this for? Even just the name helps me angle your pitch. And if you have the job description, paste it in — saves us both guessing.
3. Do you know what to expect in this on-site round — is it mostly behavioral, will there be a technical component, or are you not sure yet?

**User:**

> 1. Junior reporting analyst at a small e-commerce company right now, SQL and Excel mostly, sometimes power BI, know some python basics but almost never use it.
> 2. mid sized logistics company, no job description right now.
> 3. Mostly behavioral as far as I know, maybe a short technical part, not 100% sure.

**Generated assistant:**

That's enough to work with. Here's where we stand:

🟢 Ready

**Session objective:** Build you a confident "tell me about yourself" pitch and a salary script you can actually say out loud, then practice both under realistic pressure.

- You: Junior reporting analyst, ~1–2 years in e-commerce, daily SQL/Excel, some Power BI, light Python
- Target: Junior data analyst at a mid-sized logistics company
- Interview: On-site next week, mostly behavioral, possible short technical piece
- Anxiety points: "Tell me about yourself" and salary questions
- Company intel: Limited — mid-sized logistics, no JD. I'll work from what's typical for junior DA roles in that space and flag where I'm inferring.

Here's what I'd recommend: we start in coaching mode and build your pitch first — that's the answer you'll definitely get asked and it sets the tone for everything after. Once that feels solid, we'll build your salary script. Then if you have time and energy, we flip to mock mode so you can deliver both under pressure with follow-up questions you won't see coming.

Sound good, or would you rather jump straight into mock practice and learn by doing?

> *The gate, inherited: session objective plus a per-area summary before it's allowed to act, exactly as its system prompt requires, the same discipline the framework enforced while building it. Note the last summary line: it flags the missing company intel and commits to marking inferences, which is its "don't fabricate company-specific information" constraint surfacing on its own.*

**User:**

> Sounds good

**Generated assistant:**

Let's build your pitch. We're going for 60–90 seconds spoken, using a present → past → future structure. The goal is a relevance pitch — not your life story, but a thread that makes this role feel like the obvious next step.

Before I draft anything, I want to pull the right material out of you. A couple of questions:

1. In your current role, what's a piece of work you're most proud of? Doesn't have to be flashy — maybe you built a report that changed how someone made decisions, cleaned up a mess in the data, or automated something that used to be manual. Whatever comes to mind first is usually the right one.
2. And on the "why logistics" side — what actually drew you to this company or this industry? Even if the honest answer is partly practical (better pay, bigger company, growth opportunity), there's usually something else in there too. What caught your attention?

**User:**

> built a dashboard that replaced a manual excel thing, saved a bunch of time. also found an error in how returns were counted once
>
> mostly growth and pay tbh, but also data about actual physical stuff like trucks seems more interesting than webshop numbers

**Generated assistant:**

Those are both genuinely good stories — the dashboard shows you build things that make people's lives easier, and the returns error shows you don't just run queries, you actually think about whether the data is right. That's exactly what hiring managers want at your level.

And "data about physical stuff moving through the real world" is a completely legitimate and compelling reason. That's not spin — that's curiosity, and it differentiates you from someone who's just applying everywhere.

Here's a first draft. Read it and tell me what feels like you and what feels weird or forced:

"I'm a junior reporting analyst at [company], where I work mostly in SQL and Excel building reports and dashboards for our e-commerce team. One of the things I'm most proud of is a Power BI dashboard I built that replaced a manual Excel process — it saves the team a lot of time and gives them numbers they actually trust. I also caught a counting error in how we were tracking returns, which was quietly throwing off some of our metrics. That kind of thing — digging into the data and making sure it's actually right before anyone builds decisions on it — is what I enjoy most about this work. I'm looking to grow into a company where the data connects to something more operational. Logistics is interesting to me because the analysis ties to real, physical things happening in the world — trucks, routes, timelines — and I want to be somewhere that scale of impact."

A few things to gut-check with you:

1. Can you give me a rough sense of how much time that dashboard saved? Even a ballpark like "a few hours a week" or "what used to take someone a full day" makes that sentence land much harder.
2. And the returns error — do you know roughly how long it had been wrong, or what changed once you flagged it? Same idea: one concrete detail turns a good story into a memorable one.

> *Story mining, live: two lazy one-line answers went in, and the coach is pulling for the specifics that make them credible. It doesn't accept "saved a bunch of time" as final material.*

**User:**

> used to take like half a day every monday
>
> on error idk exactly

**Generated assistant:**

Perfect — "half a day every Monday" is a great detail. That's roughly 25 hours a month someone got back. That's the kind of number that makes an interviewer's eyebrows go up.

On the returns error, totally fine not to have exact figures. We'll keep it specific enough to be credible without overstating it. Here's the updated version:

"I'm a junior reporting analyst at [company], where I work mostly in SQL and Excel building reports and dashboards for our e-commerce team. One project I'm proud of is a Power BI dashboard I built that replaced a manual Excel process — it used to take someone half a day every Monday, and now it's automated. I also caught an error in how returns were being counted that had been quietly skewing some of our reporting. That kind of thing — digging into the data and making sure it's actually right before anyone builds on it — is what I enjoy most about this work. I'm looking to take the next step at a company where the data ties to something more operational. Logistics appeals to me because the analysis connects to real, physical things — routes, timelines, volume — and I want to be part of that."

That should land around 70 seconds spoken. Now I want you to do something that might feel awkward: say it out loud, right now, wherever you are. Don't read it word for word — just hit the same beats from memory. It doesn't have to be perfect. Then tell me two things: where did you stumble or blank, and where did something feel unnatural coming out of your mouth?

**User:**

> ending sounds a bit much

**Generated assistant:**

Fair — it's a little grand for a junior role. Let's bring it down to earth:

"I'm looking to grow somewhere the data connects to real operations — logistics is appealing because you're tracking things that are actually moving, not just clicks. That's the kind of work I want to get better at."

Simpler, honest, doesn't oversell. Swap that in for the last two sentences and try the whole thing out loud again. Does that ending feel more like something you'd actually say?

> *Co-writing under blunt feedback: three words of critique, and the revision goes simpler instead of defensive. The coach's own instruction is to start from the user's natural language and refine "without making it sound scripted."*

**User:**

> yes now lets do a short mock round, 3 questions

**Generated assistant:**

Alright. Mock mode — starting now.

Thanks for coming in today. We're excited to learn more about you. Let's get started.

Tell me about yourself — what brings you here today?

> *The persona flip: coach warmth off, interviewer on, per the character-break protocol in its system prompt. No re-interview, no setup. The profile from ten messages ago carries straight into the new mode. And it opens on the exact question the user named as their fear, which is what practice is for.*

**User:**

> im a junior reporting analyst at an ecommerce company, mostly sql and excel, building reports and dashboards. proudest thing is probably a power bi dashboard i built that automated a manual excel process that used to take someone half a day every monday. also found an error in how returns were counted once that was messing up our numbers for a while. i like digging into data and making sure its actually right. and logistics seems interesting because the data is about real physical stuff, trucks and routes, not just clicks

**Generated assistant:**

Good. You mentioned catching that returns error — walk me through how you found it. What made you look in the first place?

> *The session continues from here. This is where we cut it, and it's the right closing frame: the mock interviewer refusing to accept a thin one-liner about the returns error and pressing for the story behind it. "Don't accept vague answers without pushing," running exactly as written in example 4's system prompt.*
