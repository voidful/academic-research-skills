---
name: professor-fit-analyzer
description: analyze a professor from google scholar, publication lists, personal websites, lab pages, dblp, semantic scholar, arxiv, and paper pages to evaluate research strength, mentoring quality, collaboration network, lab resources, research taxonomy, future directions, applicant fit, outreach emails, and interview strategy. use when the user wants to assess whether a professor or lab is worth applying to, compare advisors, prepare a cold email, infer future research openings, or build a structured dossier from public academic evidence.
license: MIT
compatibility: claude-code, codex-cli, gemini-cli, agentskills-compatible
---

# Professor Fit Analyzer

Build an evidence-based dossier for a professor and convert that dossier into an application or collaboration strategy.

This skill is platform-agnostic. Use the browsing, search, and file-reading tools available in the current agent. Prefer public academic sources first. If browsing is unavailable, ask the user for links, PDFs, or a publication list and continue with partial coverage rather than guessing.

## Input Specification

### Required inputs
- Professor name.
- At least one of: Google Scholar URL, personal website URL, lab website URL.

### Optional but recommended inputs
- User education background (current degree, field, institution).
- User research experience (past projects, publications, technical skills).
- Application type: PhD student, master student, RA, postdoc, visiting scholar, or research collaborator.
- User strengths and distinctive capabilities.
- Nationality, language proficiency, and whether scholarship or visa sponsorship is needed.
- Target timeline (e.g., Fall 2027 PhD application, this summer for internship, immediate contact).

### Input handling rules
- If the user provides only a professor name with no URL, ask for at least one URL or publication source before proceeding.
- If user background is missing, produce conditional advice by applicant type rather than generic praise.
- If target timeline is missing, assume general exploration and skip urgency-dependent advice.
- If the user provides a CV or publication list, use it to strengthen fit analysis.

## Language Policy

Default output language is Traditional Chinese (繁體中文).

Exceptions — keep in English:
- paper titles,
- venue names (e.g., NeurIPS, ACL, CVPR),
- method and model names (e.g., Transformer, LoRA),
- technical terms without widely accepted Chinese translations,
- proper nouns (person names, institution names).

If the user writes in English, switch all output to English.
If the user explicitly requests a different language, follow that request.

## Operating Principles

1. Separate **facts**, **inferences**, and **speculation**.
2. Prefer repeated signals over one-off anecdotes.
3. Do not equate citation count, h-index, or raw publication count with quality.
4. Do not equate high output with good mentoring or overwork.
5. Do not equate clear writing with guaranteed teaching quality.
6. Treat authorship interpretation cautiously. State uncertainty.
7. Use the applicant's goals, risk tolerance, and background as the center of final advice.
8. Never claim to have read a paper that you could not access.

## Workflow Overview

Follow this sequence:

1. Build source coverage.
2. Construct the publication timeline.
3. Cluster papers into a research taxonomy.
4. Read papers and extract structured evidence.
5. Synthesize professor-level judgments.
6. Infer future directions and possible openings.
7. Produce applicant-fit analysis and professor-student type matching.
7B. Check for warning signs.
8. Draft tailored outreach emails.
9. Produce a conversation and interview playbook.
10. End with actionable next steps.

If the professor has a very large corpus, do not silently downsample. Use the coverage policy below.

## Coverage Policy

### Default target
Aim to cover the full publication list that is realistically accessible.

### When the corpus is large
If the professor has too many papers to fully inspect in one pass, use a transparent tiered policy:

- **Tier 1: Core papers**. Recent papers, highly central papers, representative papers from each research line, and papers that appear to define transitions.
- **Tier 2: Supporting papers**. Additional papers needed to validate taxonomy, collaboration patterns, and student trajectories.
- **Tier 3: Peripheral papers**. Minor, redundant, workshop, demo, or inaccessible papers. Summarize these more lightly.

Always report:
- how many total papers were identified,
- how many were read in depth,
- how many were skimmed or inferred from metadata,
- which conclusions depend on partial coverage.

## Source Collection Protocol

Prioritize these sources in roughly this order:

1. Google Scholar profile or publication list.
2. Personal website and lab website.
3. DBLP or field-specific bibliographic pages.
4. Official paper pages and proceedings.
5. arXiv versions when official full text is unavailable.
6. Semantic Scholar or other metadata aggregators.
7. Student pages, alumni pages, CVs, group news, and grant or project pages.

For each source, extract what it is good at:

- **Scholar**: breadth, counts, timeline.
- **Personal or lab website**: group structure, students, projects, funding clues.
- **DBLP**: cleaner metadata and venue history.
- **Official proceedings**: authoritative venue and full text.
- **arXiv**: accessible full text and appendices.
- **Student or alumni pages**: student identity and trajectory clues.

When sources disagree, prefer the most authoritative source and mention the conflict.

## Step 1. Build the Professor Snapshot

Start by compiling:

- name, institution, department, lab name,
- research areas,
- public student or alumni lists,
- recent job title or affiliation,
- publication count by year,
- top recurring venues,
- recurring coauthors,
- visible grants, datasets, systems, or infrastructure clues.

Then create a one-paragraph summary of the professor's apparent academic identity.

## Step 2. Build the Research Timeline

Organize papers by year and note:

- publication count per year,
- venue mix,
- first-author and last-author patterns,
- recurring student names,
- recurring collaborators,
- emergence or decline of themes,
- bursts near a specific conference cycle.

Look for transitions:

- early phase,
- consolidation phase,
- expansion phase,
- recent pivot.

## Step 3. Build the Research Taxonomy

Cluster papers into a coherent research system rather than a flat list.

Required buckets:

1. core research lines,
2. secondary lines,
3. application branches,
4. shared methodological spine,
5. recent pivots,
6. likely expansion directions.

For each cluster, identify:

- founding papers,
- continuation papers,
- turning-point papers,
- side explorations,
- possibly opportunistic or trend-following papers.

Use repeated problem statements, methods, datasets, and coauthor patterns to justify the taxonomy.

## Step 4. Read Papers and Extract Structured Evidence

For each paper, produce the following fields.

### Paper metadata
- title
- year
- venue
- author list
- corresponding author or last author position when visible
- likely lead type: student-led, professor-led, externally-led, or unclear

### Problem
- what core problem the paper tries to solve
- why that problem matters
- what bottleneck existed at that time

### Method
- what solution the paper proposes
- the central idea
- the important design decisions
- why those design decisions make sense

### Novelty
Classify the paper's main novelty as one or more of:
- problem framing
- conceptual insight
- model design
- training recipe
- data processing
- benchmark or dataset
- system building
- theoretical analysis
- empirical discovery
- scale or infrastructure

### Resources
Estimate what the work likely required:
- dataset scale,
- compute scale,
- special hardware,
- expensive equipment,
- annotation effort,
- industrial or clinical access,
- cross-institution coordination,
- engineering infrastructure.

Mark resource claims as **directly stated** or **inferred**.

### Authorship analysis
Use repeated evidence to infer:
- likely students,
- likely postdocs or senior collaborators,
- internal collaborators,
- external academic collaborators,
- industrial collaborators,
- one-off versus long-term partners.

Do not over-interpret a single author order pattern.

### Impact and signal
State whether the paper appears to be:
- a core paper for the professor,
- a representative student paper,
- a collaboration-heavy paper,
- a transition paper,
- a prestige venue signal,
- a strong indicator of advising or resource access.

### Writing quality
Judge:
- whether the introduction states the problem clearly,
- whether the related work builds context well,
- whether the method is explained clearly,
- whether the experiments are rigorous,
- whether the paper shows pedagogical clarity.

### Confidence
Assign high, medium, or low confidence and explain why.

For all paper-level judgments, use the evidence rubric in [references/evidence-rubric.md](references/evidence-rubric.md).

## Step 5. Synthesize Professor-Level Judgments

After reading across papers, evaluate the professor along these dimensions.

### Research strength
Assess:
- importance of chosen problems,
- persistence on valuable questions,
- ability to define agendas rather than follow trends,
- ability to produce influential methods,
- venue consistency,
- long-term coherence.

### Mentoring strength
Assess:
- number and stability of probable students,
- whether students appear as first authors,
- whether students grow over time,
- whether students lead increasingly mature work,
- visible alumni outcomes when available,
- whether the professor seems to create independent researchers.

### Collaboration network
Assess:
- cross-lab, cross-university, cross-country, and industry collaborations,
- breadth versus depth,
- repeated high-quality collaborators,
- whether the professor appears central or peripheral in collaborations.

### Resource profile
Assess:
- compute access,
- special equipment,
- unique datasets,
- industry or institutional access,
- ability to run costly experiments,
- efficiency of converting resources into strong outputs.

### Workload and culture risk
Assess cautiously:
- bursts of many papers in one cycle,
- high throughput patterns,
- slicing risk,
- signs of mature delegation,
- signs of deadline-driven culture,
- whether multiple interpretations remain plausible.

Always include at least two plausible explanations for a high-output signal when the evidence is ambiguous.

### Teaching and communication signal
Assess from writing and exposition:
- introduction clarity,
- related-work organization,
- method explanation,
- figure pedagogy,
- whether the papers appear suitable for training newcomers.

## Step 6. Infer Future Directions and Openings

Use the following signals:
- future-work statements,
- research shifts in the last two to three years,
- new coauthor patterns,
- new datasets or systems,
- repeated unresolved bottlenecks,
- repeated methods or application patterns.

Answer:
- where the professor is most likely to expand,
- where new students or collaborators are most likely needed,
- which directions are durable,
- which directions may be opportunistic rather than strategic.

## Step 7. Fit Analysis for the Applicant

Map the applicant to one or more of these roles:
- fast experimentalist,
- theory builder,
- systems or engineering contributor,
- data or benchmark builder,
- cross-domain bridge,
- application specialist.

Then judge:
- why this professor is a good fit,
- why this professor may be a risky fit,
- how hard the application may be,
- what the applicant should emphasize,
- what gaps the applicant should fix before reaching out.

If the applicant background is missing, give conditional advice by applicant type instead of generic praise.

### Professor-student type matching

Evaluate what TYPE of student is most likely to thrive under this professor:

- **free explorer** who generates own questions vs. **structured-problem student** who needs clear direction,
- **engineering-strong but theory-weak** vs. **theory-oriented**,
- **fast-publication seeker** who wants rapid output vs. **deep-diver** who wants long-term foundational work,
- **independent worker** who runs with minimal guidance vs. **frequent-guidance seeker**,
- **broad learner** who wants exposure to many topics vs. **narrow specialist**.

Then, if the user's background is available, map the user to these types and assess match quality. Highlight mismatches as risks, not disqualifications — some mismatches are growth opportunities.

## Step 7B. Warning Signs

Before finalizing fit analysis, explicitly check for these red flags. This section must always appear in the output, even if no warning signs are found.

### Research direction mismatch
- The professor's core direction has shifted away from the applicant's interest area in the last 2-3 years.
- The research line the applicant cares about has no recent papers.

### Student development concerns
- Few or no student first-author papers in recent years.
- No visible growth trajectory for current students (students never progress from middle author to lead author).
- No visible alumni outcomes, or alumni have left the field without clear career paths.

### Collaboration dependency
- The professor's recent high-impact work depends heavily on one specific external collaborator or institution.
- Risk: if that collaboration ends, the research line may stall, leaving current students stranded.

### Lab dynamics signals
- Very high student turnover inferred from rapidly changing author lists.
- Single-student lab with no visible peer cohort.
- Publication patterns suggesting paper-slicing or salami publishing.

### Presentation rules for warning signs
- List each warning sign found with supporting evidence and evidence level (A/B/C/D).
- For each, state severity: **blocking** (strongly reconsider), **serious** (proceed with caution), or **minor** (be aware).
- For each, state whether there is a plausible benign explanation.
- If no warning signs are found, state that explicitly rather than omitting the section.

## Step 8. Outreach Email Strategy

Use the rules in [references/outreach-playbook.md](references/outreach-playbook.md).

Always tailor the message around:
- one or two concrete research lines,
- one concrete way the applicant can contribute,
- one signal of serious homework,
- one mutually beneficial reason to talk.

Avoid:
- generic flattery,
- vague statements like “I am interested in your research”,
- copying paper summaries into the email,
- asking for admission without showing fit.

Produce three versions when the user requests outreach support:
- prospective student email,
- research collaboration email,
- short relationship-building email.

## Step 9. Conversation and Interview Playbook

When the user requests meeting preparation, include:
- likely questions from the professor,
- what each question is testing,
- strong answer structure,
- failure modes,
- one or two smart questions the applicant should ask,
- how to pitch a small research idea without sounding naive or arrogant.

### Counter-questioning strategy
Provide questions the applicant can ask to probe:
- mentoring style: "What does a typical first-year project look like?" / "How do students choose topics?"
- lab culture: "What does a typical week look like for your students?" / "How does the group handle conference deadlines?"
- actual availability: "How often do you meet with students one-on-one?" / "Do students collaborate with each other?"

Frame these so the applicant sounds curious, not interrogating.

### Building match feeling in a short meeting
Structure a 20-minute conversation:
1. (2 min) Open with a specific observation about their recent work — not flattery, but genuine insight or question.
2. (5 min) Connect your background — one project, one skill, one link to their research.
3. (5 min) Float a small research angle you have been thinking about.
4. (5 min) Ask for the professor's perspective — "Where do you see this heading?" / "What is the bottleneck?"
5. (3 min) Close with practical next steps — "Would it help if I read X before we talk again?"

### Research idea pitch calibration
- The idea should be small enough to be feasible as a starter project.
- It should connect to the professor's existing line but add a twist from your own background.
- Frame it as "I have been thinking about X and would love your perspective" — not "I want to do X in your lab."
- Prepare for the professor to redirect or dismiss it. That is also valuable information about how they engage with new ideas.
- Avoid ideas that are too ambitious (signals naivety) or too incremental (signals lack of vision).

## Output Contract

Use the template in [references/output-template.md](references/output-template.md).

At minimum, include these sections when enough evidence exists:

1. Professor Snapshot
2. Research Timeline
3. Research Taxonomy
4. Paper-by-Paper Analysis
5. Advisor Assessment
6. Future Directions
7. Fit Analysis for the Applicant
8. Warning Signs
9. Cold Email Templates
10. Conversation and Interview Playbook
11. Final Verdict

If some sections cannot be completed, keep the section title and explicitly state what is missing.

## Final Verdict Requirements

End with:
- what type of applicant is most likely to thrive with this professor,
- what type is least likely to thrive,
- the strongest opportunity,
- the biggest risk,
- the next three actions the user should take.

## Guardrails

- Do not present speculation as fact.
- Do not infer workload, personality, or ethics from a single paper.
- Do not assume all recurring coauthors are students.
- Do not assume that all last-author papers are fully driven by the professor.
- Do not hide access limits or incomplete coverage.
- Do not fabricate alumni outcomes.
- Do not optimize for praise. Optimize for decision usefulness.

## References

- [references/evidence-rubric.md](references/evidence-rubric.md). Evidence ladder, confidence rules, and counter-evidence protocol.
- [references/output-template.md](references/output-template.md). Default report structure.
- [references/outreach-playbook.md](references/outreach-playbook.md). Email and interview strategy rules.
