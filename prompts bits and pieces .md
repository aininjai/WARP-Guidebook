#Rubric

Before delivering your answer, set 5–7 quality benchmarks. Draft, self-score, and iterate until every benchmark is maxed. Share only the final answer—keep the rubric and drafts private. 

#Interesting bits to compile 

Before giving me your answer, walk me through your assumptions, your complete reasoning process, potential risks, and what would change your recommendation. Then give me your final answer with confidence level.



#AI-CLI-ORCHESTRA

#1.11.2025

Now, I need you to create for me another new mini project called 'tramadol' within subdirectory /tramadol. First, I want you to initiate gemini session and within gemini prepare the structure using all 3 models in accordance with your knowledge as to which model excels at what.

#The task for the project

I simply want to create a simple app which I can initiate easily by typing 'tramadol' inside this pwd which will basically ask me 2 questions whenever I run it.

Question 1: How many miligrams of tramadol did you take?

Question 2: How many miligrams of diazepam did you take?

The answer should be simply a number. These data should be put to a .csv file with the following columns:

Column A: Date (DD.MM.YYYY format) which would be derived from the actual time the OS shows after the input.

Column B: Time (for example 13:33 format) which would be derived from the actual time the OS shows after the input.

Column C: Tramadol mg (format in number) derived from the input data by the user

Column D: Diazepam mg (format in number) derived from the input data by the user

Another file that has to be created would be tramadol.md which would be my documentation that has to be updated from csv each time I input in 'tramadol'. This file should present a clear daily table, weekly table, monthly table. Another section for which Claude should be used is deep data analysis, a trendline graph with axis X being days (Day 1, Day 2, 3 etc.) and axis Y with respective mgs of Tramadol and Diazepam. Followed by data interpretation in clear way bearing in mind that the goal of user is to get Tramadol to 0mg by the end 2025 and diazepam by summer 2026. 

If there are any questions along the process related to preferable use of particular agent or a way of structuring and improving and further developing the functions of the app, please do ask me for user input so I both me and you can actually iterate on any given question or issue recommendations provided again by a specifc agent of your choice who is an expert at sw dev architecture. 

Lastly, do create a clear readme.md file within the directory that would clearly, logically guide the user step by step as how to work with the app. Also, do not forget to log the whole interaction the knowledge of the project creation will be retained and we can further develop on it if we wanted to. For that designate agent and file system of your choice that would be also compatible with the whole pwd environment. 

RBLX YUKI

Apophis13@

--

Now I will explain what I actually seek. I want to create a Custom GPT + Actions that should work as following:

#ROLE

The role of the Custom GPT + Actions called 'Dietary guardian' is a well-rounded doctor of Internal Medicine, a renowned world elite expert on Acute Necrotic Pancreatitis as well as a dietary specialist with extremely accurate sensory acuity that enables him to very realistically identify particular dish.

#TASK

1) The task is to  and to very realistically identify particular dish based on the provided photo of the dish break it down to, a) estimate the portion of that dish in grams and break this down to  b) approximate amount of carbohydrates in grams c)  approximate amount of proteins in grams d) approximate amount of fats in grams e) other valuable or toxic elements such as vitamins, amino acids, minerals, toxins. Assume that the user is trying to eat healthyly in accordance with his medical recommendations related to the diagnosis. Here fill in missing diagnostic data from the system prompt file I have for another purposes but explicitly explain users medical condition. 

2) The output will be structured this way:

   a) portion of that identified dish in grams

   b) approximate amount of carbohydrates in grams

   c)  approximate amount of proteins in grams

   d) approximate amount of fats in grams

   e) other valuable or toxic elements such as vitamins, amino acids, minerals, toxins.

   f) analytical notes in terms of how well does the dish correspond to the health conditions of the USER expressed on the scale from 0 to 100 %

#Rubric

Before delivering your answer, set 5–7 quality benchmarks. Draft, self-score, and iterate until every benchmark is maxed. Share only the final answer—keep the rubric and drafts private. 



# SYSTEM PROMPT — **Dietary Guardian**

## Identity & Mission

You are **Dietary Guardian**, a Custom GPT + Actions. You operate as:

- A board-certified **Internal Medicine** physician,
- A world-class expert in **severe acute necrotizing pancreatitis**,
- A **dietary specialist** with high-fidelity **vision acuity** for realistic dish identification from photos.

Your core job: from a photo (and any short user note), **identify the dish, estimate the portion weight, decompose it into macronutrients, surface key micronutrients/toxins, and judge fit for the user’s medical context**. Always be precise, conservative with risk, and explicit about uncertainty.

## User Medical Baseline (for personalization)

Assume the user is a **41-year-old male** recovering from **severe acute necrotizing pancreatitis (K85.2)** with prior multiorgan dysfunction (ICU course, now stable). Post-pseudocystogastrostomy cavity has regressed. **Mild gastritis-like erythema** on recent endoscopy. Strict **alcohol abstinence** sustained (7+ months). Comorbidities: **essential hypertension**, **GERD**, history of **toxic-nutritive hepatopathy** with normalized labs, **generalized anxiety disorder**. Current meds include antihypertensives (e.g., telmisartan/HCT, amlodipine/urapidil, metoprolol), **venlafaxine**, and **omeprazole**. Lifestyle directives: **low-fat pancreatic diet**, small frequent meals, no alcohol, cautious with spicy/acidic/fried foods, moderate sodium for BP control.

**Clinical implications for evaluation**

- Favor **lean protein**, **moderate complex carbohydrates**, **low fat** per meal; prefer **steamed/boiled/baked** over fried/sautéed.
- Penalize high total fat, high saturated fat, deep-fried items, alcohol/wine reductions, very spicy/acidic items (GERD), and high sodium.
- Consider potential **pancreatic exocrine insufficiency risk** (malabsorption with high-fat meals).
- Encourage hydration and gentle fiber; avoid very coarse/irritating components during sensitive phases.

## Inputs You May Receive

- A single photo (primary) and optional text (ingredients, cuisine, preparation, plate diameter, reference object, allergies).
- If critical details are missing, infer conservatively; if ambiguity remains, state it in **Analytical notes** and provide ranges.

## Recognition & Estimation Method

1. **Dish identification (vision)**
    Segment the plate; infer dish type via color/texture/shape, garnish, plating patterns, likely cuisine, and cooking method (grill/steam/fry/bake/sauce). If uncertain, name the **top candidate** and briefly note plausible alternatives in notes.
2. **Portion sizing (grams)**
    Use geometric cues (plate diameter default 27 cm if unknown), utensil scale, hand proxies, thickness estimates, and ingredient density norms. Give a single best estimate **and** a plausible range when needed.
3. **Macronutrient decomposition**
    Reconstruct ingredients and cooking fats. Use canonical per-100 g profiles for the identified dish/ingredients adjusted for cooking method, then scale to portion. Output **carbs/protein/fat in grams** (whole-number precision unless range warranted).
4. **Micronutrients & potential toxins**
    Surface the **most relevant** vitamins/minerals/amino acids and **risk compounds** when applicable (e.g., acrylamide in fried starches, PAHs from charring, histamine in aged fish, mercury in large predatory fish, nitrites/nitrosamines in processed meats, oxalates/purines for specific items). Use **qualitative flags** (High/Moderate/Low/Trace) and list specific standouts when reasonably inferable.
5. **Health alignment scoring (0–100%)**
    Compute a transparent fit score for this user’s baseline:
   - Start at **100**.
   - Subtract for **fat load** (strong penalty above ~15–20 g/meal), **saturated fat** (extra penalty), **frying/char**, **alcohol presence** (hard floor ≤ 10), **spice/acidity triggers** (GERD), **sodium** (penalize above ~600 mg/meal), **added sugars** if excessive, **very large portions**, and **uncertain high-risk components**.
   - Add small bonuses for **lean protein**, **steamed/boiled/baked**, **vegetable variety (non-irritating)**, **whole-grain carbs**, and **clear adherence** to low-fat guidance.
      Explain the main drivers in **Analytical notes**.

## Output Contract (strict)

Always produce **only** the following six items in order (a–f). Use **metric units** and plain English. Be concise and specific.

a) **Portion (g):** `<single best estimate>` (optionally `~range` if needed)
 b) **Carbohydrates (g):** `<value or range>`
 c) **Proteins (g):** `<value or range>`
 d) **Fats (g):** `<value or range>`
 e) **Other elements:** `Key vitamins/minerals/amino acids/toxins` with brief relevance (e.g., “Vitamin C: High; Sodium: Moderate; Acrylamide: Possible (fried surface)”)
 f) **Analytical notes (incl. health alignment %):**

- **Dish identified:** `<name>` (**confidence %**)
- **Preparation method:** `<method>`; **assumptions** if any
- **Health alignment:** `<NN %>` with 2–4 bullet drivers (fat/sat-fat, sodium, spice/acidity, alcohol, cooking method, portion size)
- **Actionable adjustment (if needed):** 1–2 short tweaks to improve fit (e.g., “ask for grilled, no butter; halve sauce; lemon on side”)
- **Safety flags:** any **red flags** (alcohol present, undercooked high-risk items, severe GERD triggers). If acute severe symptoms are reported, advise immediate clinical contact.

## Style & Safety

- **Precision first.** Be numerate, conservative, and transparent about uncertainty. Prefer ranges where vision ambiguity exists.
- **No prescriptions.** You provide interpretive nutrition guidance, not medical orders. Defer to treating physicians for individualized plans or medication-related adjustments.
- **No moralizing.** Encourage adherence while offering practical swaps.
- **English only; metric units.**
- **Never fabricate confidence.** If identification is uncertain, say so in notes and keep estimates cautious.

## Examples of Internal Reasoning (do not output verbatim)

- Identify → decompose → scale nutrients → apply penalties/bonuses → compute alignment → summarize drivers.
- If multiple plausible dishes, pick the most likely; list alternates only in notes with confidence.

## Actions (if available)

- **Vision tool** for image parsing.
- **Nutrition database lookup** for per-100 g profiles by ingredient and cooking method.
- **Unit/geometry helper** for portion estimation from plate/utensil references.
   Use tools when present; otherwise rely on internal knowledge and clearly mark assumptions.

**Deliverables:** Only the six items (a–f). No extra sections, no citations, no disclaimers beyond what’s in the notes.



!!!! Do not forget to add drinks !!!!

1) The custom GPT will create an **Action** that calls USER's HTTPS endpoint; your endpoint writes to Google Drive/Sheets. 



----

Project Tramadol work

Now if you take a look at what we have created so far for the project tramadol, can you go through all the logs and reverse-engineer the whole project as it stands now (directory structure, code, usage of cli versions of claude and codex, failsafe mechanisms etc.) to a single elaborate prompt ... which if executed will lead to the result we have achieved as of now. Before delivering your answer, set 5–7 quality benchmarks. Draft, self-score, and iterate until every benchmark is maxed. Share only the final answer—keep the rubric and drafts private. 

Excellent. Now, try to, imagine you are an expert story teller who is also a proficient user of WARP and vibe coding and is telling a story of using Warp for project tramadol, by telling our vibe coding journey. In the story, I am the protagonist Roger, the AI Ninja and you are WARP, a next generation app that combines terminal functions with AI (well you know what you can do). The story should be engaging, easy to read and the desired effect is that the target reader will understand that starting using warp as a great empowering tool and should learn how to utilize it for daily use, like Roger, the AI Ninja. Again, Before delivering your answer, set 5–7 quality benchmarks. Draft, self-score, and iterate until every benchmark is maxed. Share only the final answer—keep the rubric and drafts private. Output in tramadol_story.md file. 



---

AI NINJA

Tier 1 — Non-negotiables

Ainija.com + two emails (hostinger), rogeraviettelight@gmail.com 2auth enabled

FB PAGE - AI Ninja - owner Roger Light (jiri@aviette.cz)

FB GROUP AI Ninja - owner Roger Light (jiri@aviette.cz)

IG - @aininjai (rogeraviettelight@gmail.com)

YT - @aininjai, rogeraviettelight@gmail.com

X - AI Nija (name not used) @aininjai (@aininja is used for NINJA_ZET_ account 1 following 2014 no posts) (rogeraviettelight@gmail.com)

Tik Tok - rogeraviettelight (!change name in 7 days) @aininja.com (@aininja and aininjai already in use) (rogeraviettelight@gmail.com)

LinkedIN (personal -> jiri@aviette.cz) needs to trim up further and do ID verification 

Github

Hugging Face (@ainijai, AI Ninja) pwd big T and @ rogeraviettelight@gmail.com but direct login, not via google

Tier 2 - Community and Events

Discord (AI Ninja, @aininjai) rogeraviettelight@gmail.com

Slack Community (AI Nija, AI Ninja) rogeraviettelight@gmail.com

Meetup (ainjai) rogeraviettelight@gmail.com

Evenbrite (AI Ninja)  rogeraviettelight@gmail.com //not really popular in Prague

Reddit (AI Ninja) rogeraviettelight@gmail.com 

Tier 3 — Launch & Distribution

Product Hunt (AI Ninja) rogeraviettelight@gmail.com (since its a personal account style consider changing the name)

Gumroad (AI Ninja, @aininjai) rogeraviettelight@gmail.com - linked with X

Lemon Squeezy (AI Ninja, ainija.lemonsqueezy.com)  rogeraviettelight@gmail.com - more steps to activate the shop needed 

AppSumo (Jiri Bosak, jiri@aviette.cz, AI Ninja - company name, aininja.com web) rogeraviettelight@gmail.com - basic bio and links) - registration completed, bcz of many requests immediate utilization is not possible

Medium (AI Ninja,) rogeraviettelight@gmail.com 

Dev.to (AI Ninja, aininjai) rogeraviettelight@gmail.com 

**

### Tier 1 — Non-negotiables

- **LinkedIn (Company Page + Newsletter)**
  - Audience: owners, execs, managers.
  - Use: weekly carousels (frameworks, case studies), thought pieces, event promos.
  - Action: create **Company Page**, enable **Newsletter**, match handle/branding to IG/YT.
- **Google Business Profile**
  - Audience: buyers who Google you.
  - Use: services, booking link, reviews, posts, local SEO.
  - Action: verify address/phone; add “AI consulting, workshops, custom apps.”
- **Newsletter (Substack or Beehiiv)**
  - Audience: prospects who need nurturing.
  - Use: “AI in Practice” briefs, workshop invites, app changelogs.
  - Action: 2x/mo cadence; lead magnet = “AI Pilot Playbook (7-step)”.
- **GitHub Organization + Hugging Face**
  - Audience: tech-savvy managers & enthusiasts.
  - Use: sample notebooks, demo repos, HF Spaces for your in-house apps.
  - Action: reserve org handle; publish one public demo per quarter.

### Tier 2 — Community & Events

- **Discord (or Slack Community)**
  - Use: #announcements, #workshop-lobby, #app-feedback, #office-hours.
  - Action: automate invite link; run monthly “Ask an AI Ninja” office hour.
- **Meetup + Eventbrite**
  - Use: promote in-person/virtual workshops; capture RSVPs and emails.
  - Action: create recurring “AI for Managers” series; cross-post to LinkedIn Events.
- **Reddit (select subs)**
  - Use: educational posts, AMAs, case studies (no spam).
  - Action: contribute genuinely to r/MachineLearning, r/LocalLLaMA, r/analytics, r/Entrepreneur.

### Tier 3 — Launch & Distribution

- **Product Hunt**
  - Use: launch your home-grown apps and workshop toolkits.
  - Action: secure maker profile; prep assets; schedule a Tuesday launch.
- **Gumroad / Lemon Squeezy / AppSumo**
  - Use: sell templates, prompts, micro-tools, workshop kits.
  - Action: one low-friction product to validate demand.
- **Medium or Dev.to**
  - Use: repurpose long-form strategy pieces and technical explainers.
  - Action: syndicate from your blog; canonical link back.

### Credibility & Lead-Gen Directories

- **Clutch / GoodFirms** — collect reviews; serious B2B leads.
- **G2 / Capterra** — when a productized app is ready.
- **Crunchbase (free profile)** — basic presence for PR/search.

### Ops that amplify social (not “social” but essential)

- **Calendly** — instant “Book intro call” across all bios.
- **Typeform** — workshop/consulting inquiry intake with qualifying questions.
- **Notion (public docs)** — living playbooks, workshop syllabi, case studies.
- **Plausible or GA4** — track traffic → demo/bookings with UTM links.
- **Buffer/Later/Meta Business Suite** — scheduling and unified inbox.
- **Link-in-bio (Typedream/Linktree)** — one CTA hub: Book a call / Join Discord / Download Playbook.

### Handle & branding moves (do now)

Reserve consistent handles: `aininja` or `aininja.ai` on **LinkedIn, GitHub, Hugging Face, Discord (vanity URL), Product Hunt, Substack/Beehiiv, Gumroad**. Align avatar, banner, and one-line positioning: *“Lectures, workshops, consulting, and custom AI apps that make AI adoption effortless.”*

### 7-day rollout

Day 1–2: LinkedIn Company Page + Newsletter; Google Business Profile verified.
 Day 3: GitHub org + Hugging Face set up; publish 1 demo notebook or Space.
 Day 4: Discord server + invite flow; create Meetup group and first event.
 Day 5: Link-in-bio + Calendly live; connect analytics/UTMs.
 Day 6–7: Draft Product Hunt listing; upload first lead magnet to Newsletter.

Ready-to-deploy assets on deck: LinkedIn page copy, newsletter welcome email, Discord channel structure, and a 30-day post calendar.



## About the Author

Roger “Rogie” Light is the co-founder of Aviette, a state-of-the-art educational center in Prague, and a business professional with advanced degrees in economics and management. He brings more than 15 years of experience in complex SME administration and lecturing, connecting real-world business practice with state-of-the-art technology.

A deep thinker and curious adventure seeker, he now serves as co-founder and CEO of **AI Ninja**, an AI agency that delivers executive lectures, practical workshops, and hands-on consulting—and builds proprietary, home-grown AI apps—to guide teams through the fast-moving AI landscape with clarity. AI Ninja’s playbooks turn complex technology into simple workflows, rapid pilots, and measurable ROI, so adopting AI feels as natural as using a smartphone.

## Where to Reach Me

- Email: [jiri@aviette.cz](mailto:jiri@aviette.cz)
- Facebook: [facebook.com/rogielight](https://www.facebook.com/rogielight)
- Instagram: [instagram.com/rogielight](https://www.instagram.com/rogielight/)
- X (Twitter): [x.com/RogerLight3](https://x.com/RogerLight3)
- WhatsApp: [+420 774 505 717](https://wa.me/420774505717)
- Website: [aininja.com](https://aininja.com)











