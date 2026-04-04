---
name: professor-fit-analyzer
description: analyze a professor from google scholar, publication lists, personal websites, lab pages, and field-specific bibliographic databases (e.g., DBLP, PubMed, SSRN, PhilPapers, MathSciNet, arXiv, Scopus) to evaluate research strength, mentoring quality, collaboration network, lab resources, research taxonomy, future directions, applicant fit, outreach emails, and interview strategy. designed for students at all levels — PhD applicants, master's students, and undergraduate researchers (capstone/thesis/independent study) — across all academic disciplines. use when the user wants to assess whether a professor or lab is worth applying to, compare advisors, prepare a cold email, find a thesis or capstone advisor, infer future research openings, or build a structured dossier from public academic evidence.
license: MIT
compatibility: claude-code, codex-cli, gemini-cli, agentskills-compatible
---

# Professor Fit Analyzer

Build an evidence-based dossier for a professor and convert that dossier into an application, advising, or collaboration strategy.

This skill is platform-agnostic, discipline-agnostic, and level-agnostic. It serves PhD applicants, master's students seeking thesis advisors, and undergraduate students looking for capstone/thesis/independent-study supervisors — across all academic fields. Use the browsing, search, and file-reading tools available in the current agent. Prefer public academic sources first. If browsing is unavailable, ask the user for links, PDFs, or a publication list and continue with partial coverage rather than guessing.

## Input Specification

### Required inputs
- Professor name.
- At least one of: Google Scholar URL, personal website URL, lab website URL.

### Optional but recommended inputs
- User education background (current degree, field, institution).
- User research experience (past projects, publications, technical skills).
- Application type: PhD student, master's student (thesis-track or coursework-track), undergraduate researcher (capstone/thesis/independent study/專題), RA, postdoc, visiting scholar, or research collaborator.
- User strengths and distinctive capabilities.
- Nationality, language proficiency, and whether scholarship or visa sponsorship is needed.
- Target timeline (e.g., Fall 2027 PhD application, this summer for internship, immediate contact).

### Input handling rules
- If the user provides only a professor name with no URL, ask for at least one URL or publication source before proceeding.
- If user background is missing, produce conditional advice by applicant type and level rather than generic praise.
- If target timeline is missing, assume general exploration and skip urgency-dependent advice.
- If application type is missing, ask the user to specify their level (PhD / master's / undergraduate / other). The analysis depth and advice framing differ significantly by level.
- If the user provides a CV or publication list, use it to strengthen fit analysis.

## Language Policy

Default output language is Traditional Chinese (繁體中文).

Exceptions — keep in English:
- paper titles,
- venue names (e.g., NeurIPS, ACL, Nature, The Lancet, American Economic Review),
- method and model names (e.g., Transformer, CRISPR, difference-in-differences),
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
6. Treat authorship interpretation cautiously. State uncertainty. Authorship norms vary by field (see Field Profile below).
7. Use the applicant's goals, risk tolerance, level, and background as the center of final advice.
8. Calibrate analysis depth and advice to the applicant's level (see Applicant-Level Calibration below).
9. Never claim to have read a paper that you could not access.

## Workflow Overview

Follow this sequence:

0. Detect the academic field and establish field-specific conventions.
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

## Applicant-Level Calibration

The analysis depth, fit analysis, outreach strategy, and advice framing should adapt to the applicant's level **and field**.

### PhD applicant
- Full-depth analysis is appropriate.
- Evaluate long-term research trajectory fit (3-5+ years).
- Emphasize mentoring quality, student outcomes, publication opportunity, and advisor-student working style.
- Outreach should demonstrate research maturity and concrete contribution.
- Warning signs about student development and lab culture deserve full scrutiny.
- **Humanities/social sciences**: PhD duration is often 5-7+ years. Advisor fit is about intellectual compatibility, theoretical alignment, and mentoring on writing and argumentation — not just "research output." Publication expectations during the PhD vary widely.
- **Biomedical sciences**: PhD involves extensive lab rotations and bench work in many programs. Evaluate whether the professor has wet-lab or clinical resources, and whether students get first-author papers on substantial projects (not just middle-author credits on large-team papers).

### Master's student (thesis-track)
- Focus on whether the professor has experience advising master's theses.
- Evaluate 1-2 year fit rather than long-term trajectory.
- Emphasize: topic alignment, advisor responsiveness, graduation timeline, and whether the professor's current projects have master's-accessible entry points.
- Outreach can be more straightforward — show interest, show preparation, show willingness to learn.
- Look for whether the professor has had master's students before and what they worked on.
- **Humanities/social sciences**: A master's thesis may involve archival research, textual analysis, ethnographic fieldwork, or a philosophical argument. Look for whether the professor supervises theses in these methodologies and whether the topic scope is achievable in 1-2 years.
- **Biomedical sciences**: A master's thesis may involve a defined experimental project, a clinical data analysis, or a literature-based systematic review. Look for well-bounded experimental questions that don't require multi-year data collection.

### Master's student (coursework-track seeking a project)
- Even lighter-touch analysis.
- Focus on whether the professor has short-term projects or well-scoped problems.
- Emphasize: how quickly the student can become productive, and whether the project scope fits a semester or two.

### Undergraduate researcher (capstone/thesis/independent study/專題)
- The lightest-touch variant, but still evidence-based.
- Focus on whether the professor is known to take undergraduates, whether the research has accessible entry points, and whether the professor has a track record of mentoring at this level.
- Look for: undergraduate co-authors in past publications, mentions of undergraduate mentoring on lab/personal pages, well-scoped sub-problems.
- Outreach should be humble but specific — show knowledge of the research area, show enthusiasm, and propose a concrete skill or background the student brings.
- The fit analysis should address: learning opportunity, skill development, and whether the experience will strengthen graduate school applications or career preparation.
- Warning signs focus on: professor being too busy to mentor undergraduates, research requiring prerequisites the student lacks, or no history of undergraduate involvement.
- **Humanities/social sciences**: Undergraduate research might involve literature reviews, archival work, interview transcription and analysis, translation, or editorial assistance. The student may bring language skills, close-reading ability, cultural knowledge, or familiarity with specific historical periods or regions.
- **Biomedical sciences**: Undergraduate research often starts with assisting in ongoing experiments, learning protocols, data entry, or literature searches. The student may bring lab course experience, basic statistics, programming for data analysis, or volunteer/clinical shadowing experience.

### RA / Postdoc / Visiting Scholar / Collaborator
- Full-depth analysis similar to PhD level.
- Adjust fit analysis to the specific role.

## Step 0. Detect Academic Field and Establish Field Profile

Before proceeding, determine the professor's primary academic field from their department, publication venues, and research keywords. Then establish a **field profile** that governs how subsequent steps are interpreted.

### Field profile dimensions

Determine each of the following for the professor's field. If uncertain, state the uncertainty and use the most conservative interpretation.

**Publication culture**:
- conference-driven (CS, ML, HCI): primary outputs are peer-reviewed conference papers. Rapid cycle (6–12 months). Conference acceptance is the prestige signal.
- journal-driven (biology, medicine, physics, chemistry, economics, most social sciences): primary outputs are journal articles. Cycle 1–3 years including review. Impact factor and journal tier matter.
- monograph-driven (humanities, law, some social sciences): books and book chapters are major outputs. A single monograph may represent years of work.
- mixed: some fields (e.g., information science, education, HCI) use both conferences and journals as primary venues.

**Authorship norms**:
- first-and-last (CS, biology, biomedicine): first author did most work, last author is the PI. Middle authors contributed but did not lead.
- alphabetical (mathematics, theoretical economics, theoretical physics): author order does not imply contribution. Contribution is inferred from acknowledgments or field knowledge.
- single-author common (humanities, philosophy, mathematics): solo authorship is normal and prestigious. Few co-authored papers is not a red flag.
- large-team (high-energy physics, genomics, clinical trials): papers may have dozens to hundreds of authors. Individual contribution is hard to assess from author lists alone.

**Typical lab structure**:
- large research group (experimental sciences, ML labs): 10–30+ members including PhD students, postdocs, technicians, RAs.
- small research group (theory, humanities, some social sciences): 1–5 students. Close mentoring. Low output volume is normal.
- no lab (solo scholars in humanities, pure math): professor may work alone or with 1–2 students. Judging by "lab size" is inappropriate.

**Output volume norms**:
- high volume (ML, biomedicine): 10–40+ papers/year for a productive group is normal.
- moderate volume (most experimental sciences, social sciences): 3–10 papers/year.
- low volume (humanities, pure math, theoretical physics): 1–3 papers/year. A "slow" output rate may indicate depth, not weakness.

**Resource intensity**:
- compute-heavy (ML, computational sciences): GPU clusters, cloud compute.
- equipment-heavy (experimental physics, chemistry, biology): specialized instruments, clean rooms, wet labs.
- data-heavy (genomics, epidemiology, economics): large datasets, clinical cohorts, survey infrastructure.
- clinical-access-heavy (clinical medicine, public health, nursing research): hospital IRB access, patient cohorts, clinical trial infrastructure, medical records databases.
- fieldwork-heavy (anthropology, ecology, archaeology): field access, travel, long data collection periods.
- human-subjects-heavy (psychology, education, sociology, public health): IRB/ethics approval, participant recruitment, interview infrastructure, longitudinal cohort maintenance.
- archival/interpretive (humanities, history, law): library access, archival collections, language skills, rare manuscript access, museum or gallery collaborations.
- creative-practice (arts, design, music, creative writing, film): studio access, exhibition opportunities, performance venues, creative portfolios as scholarly output.
- minimal infrastructure (pure math, theoretical CS, philosophy): primarily intellectual resources.

**Mentoring culture**:
- structured lab meetings (experimental sciences, ML): regular group meetings, journal clubs, progress reports.
- seminar and reading group (humanities, social sciences, theoretical fields): intellectual development through discussion, close reading, and critique.
- clinical mentoring (medicine, nursing, public health): combines research mentoring with clinical training; students may have dual roles as clinicians and researchers.
- studio critique (arts, architecture, design): feedback through portfolio review, exhibition preparation, and iterative creative process.

### How the field profile affects analysis

- **Publication timeline (Step 2)**: In conference-driven fields, look for bursts near conference deadlines. In journal-driven fields, look for clusters around grant reporting periods or thesis milestones. In monograph-driven fields, gaps of 2–3 years between publications are normal. In clinical research, publication rhythm may follow clinical trial phases or cohort availability.
- **Novelty categories (Step 4)**: Use field-appropriate categories (see Step 4 below).
- **Resource profile (Step 5)**: Assess resources that matter for the field, not a generic compute checklist. For biomedical researchers, emphasize clinical access, IRB infrastructure, and funding sources (NIH, MOST, NHS, etc.). For humanities scholars, emphasize archival access, language capabilities, and institutional affiliations that enable specialized research.
- **Workload assessment (Step 5)**: Calibrate "high output" against field norms, not a universal threshold.
- **Authorship analysis (Step 4)**: Interpret author order according to field convention. In biomedicine, corresponding author (often last) is the PI; in humanities, solo authorship is the norm.
- **Warning signs (Step 7B)**: Calibrate "paper slicing" against field norms for publication granularity. In clinical medicine, separate papers per cohort or trial phase may be standard. In humanities, a single definitive article or monograph chapter may represent years of work.
- **Student skill expectations (Step 7)**: In biomedical fields, students need wet-lab or clinical skills, statistics, and often coding for bioinformatics. In humanities, students need close-reading ability, archival competence, theoretical sophistication, and often language proficiency. Do not evaluate students from one field by the skill expectations of another.

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

Prioritize these sources in roughly this order, selecting the field-appropriate ones:

1. Google Scholar profile or publication list.
2. Personal website and lab website.
3. Field-specific bibliographic databases:
   - CS/ML: DBLP, ACL Anthology
   - Biomedicine/clinical medicine: PubMed, Europe PMC, ClinicalTrials.gov
   - Public health/epidemiology: PubMed, Global Health (CABI)
   - Nursing/allied health: CINAHL, PubMed
   - Psychology: PsycINFO, PubMed
   - Social sciences/economics: SSRN, RePEc, EconLit, ProQuest Social Sciences
   - Education: ERIC, EdArXiv
   - Humanities/philosophy: PhilPapers, JSTOR, Project MUSE
   - Literature/languages: MLA International Bibliography, JSTOR
   - History: Historical Abstracts, JSTOR, digitized archives
   - Law: Westlaw, HeinOnline, SSRN
   - Arts/music: RILM, Arts & Humanities Citation Index
   - Mathematics: MathSciNet, zbMATH
   - Physics: INSPIRE-HEP, ADS
   - General: Scopus, Web of Science
4. Preprint servers (arXiv, bioRxiv, medRxiv, SSRN, EdArXiv, SocArXiv, PsyArXiv, engrXiv) when published versions are unavailable.
5. Semantic Scholar or other metadata aggregators.
6. Student pages, alumni pages, CVs, group news, and grant or project pages.
7. Funding databases (NSF Award Search, NIH Reporter, MOST 科技部計畫, ERC database, Wellcome Trust, CIHR) when visible.
8. Institutional repositories and dissertation databases (ProQuest Dissertations, university ETD repositories) — useful for identifying past students and their thesis topics.

For each source, extract what it is good at:

- **Scholar**: breadth, counts, timeline.
- **Personal or lab website**: group structure, students, projects, funding clues.
- **Field-specific databases**: cleaner metadata and venue history.
- **Official proceedings or journals**: authoritative venue and full text.
- **Preprint servers**: accessible full text and appendices.
- **Student or alumni pages**: student identity and trajectory clues.
- **Funding databases**: grant titles, amounts, and collaborators.

When sources disagree, prefer the most authoritative source and mention the conflict.

## Step 1. Build the Professor Snapshot

Start by compiling:

- name, institution, department, lab name,
- research areas,
- public student or alumni lists,
- recent job title or affiliation,
- publication count by year,
- top recurring venues (conferences, journals, book publishers, or other outlets as appropriate for the field),
- recurring coauthors,
- visible grants, datasets, systems, or infrastructure clues.

Then create a one-paragraph summary of the professor's apparent academic identity.

## Step 2. Build the Research Timeline

Organize papers by year and note:

- publication count per year (calibrated against field norms from the field profile),
- venue mix,
- authorship patterns (interpreted according to field-specific authorship norms),
- recurring student names,
- recurring collaborators,
- emergence or decline of themes,
- bursts near submission deadlines (conference cycles in CS/ML, journal special issues, grant reporting periods, or thesis completions in other fields).

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
- venue (conference, journal, book, preprint)
- author list
- corresponding author or last author position when visible
- likely lead type: student-led, professor-led, externally-led, or unclear
- (interpret authorship order according to the field profile)

### Problem
- what core problem the paper tries to solve
- why that problem matters
- what bottleneck existed at that time

### Method / Approach / Argument
- what solution, framework, or argument the paper proposes
- the central idea or thesis
- the important design decisions (for empirical/experimental work) or argumentative moves (for interpretive/theoretical work)
- why those decisions make sense
- (for humanities and interpretive social sciences: what theoretical framework or lens is used, what primary sources or cases are analyzed, what mode of argumentation is employed)
- (for biomedical research: what study design is used — RCT, cohort study, case-control, in-vitro, animal model, computational — and what are the key methodological choices)

### Novelty
Classify the paper's main novelty as one or more of the following universal categories. Use the field-appropriate examples to guide classification.

- **problem framing**: redefining or identifying a new research question
  - CS/ML: formulating a new task; humanities: proposing a new interpretive lens or reframing a canonical question; biomedicine: identifying a new clinical need or patient population; social science: revealing a previously unexamined social phenomenon
- **conceptual insight**: a new way of thinking about an existing problem
  - physics: a new theoretical prediction; economics: a new mechanism or model; literary studies: a new reading of a canonical text; medicine: a new understanding of disease mechanism
- **methodological innovation**: a new method, tool, technique, or protocol
  - CS/ML: model architecture, training recipe, algorithm; biology: new assay, imaging technique, CRISPR application; social science: new survey instrument, causal identification strategy; humanities: new digital humanities method, new archival methodology; clinical: new diagnostic protocol, new surgical technique
- **data or resource contribution**: creating or curating a valuable dataset, corpus, benchmark, code library, or shared resource
  - CS/ML: benchmark or dataset; genomics: sequenced genome; linguistics: annotated corpus; history: digitized archive; clinical: patient registry, biobank; sociology: longitudinal survey dataset
- **system or infrastructure building**: constructing a working system, platform, or pipeline
  - CS/ML: open-source toolkit, deployed system; engineering: prototype device; clinical: trial infrastructure, clinical decision support system; digital humanities: digital edition, searchable archive platform
- **theoretical analysis**: formal proofs, derivations, or mathematical frameworks
  - math: theorem; theoretical CS: complexity proof; economics: equilibrium analysis; philosophy: sustained logical argument; literary theory: new theoretical framework
- **empirical discovery**: novel findings from observation, experiment, or data analysis
  - biology: new species or mechanism; psychology: new behavioral phenomenon; astronomy: new object or signal; medicine: new clinical finding, epidemiological pattern, or drug interaction; history: newly discovered primary source evidence; sociology: previously undocumented social pattern
- **interpretive or critical contribution**: a new reading, critique, or reinterpretation of existing texts, artifacts, or cultural phenomena (primarily humanities and qualitative social sciences)
  - literary studies: new close reading of a text or corpus; history: reinterpretation of an historical event or period; art history: new analysis of an artwork or movement; anthropology: new ethnographic interpretation
- **clinical or translational contribution**: moving basic science findings toward clinical application, or evaluating interventions in patient populations (primarily biomedical)
  - medicine: clinical trial results, translational research from bench to bedside, clinical guideline development, systematic review with clinical recommendations
- **synthesis or survey**: integrating existing knowledge into a coherent framework
  - all fields: review article, meta-analysis, systematic review, handbook chapter, state-of-the-field essay

### Resources
Estimate what the work likely required. Select the resource types that are relevant to the field:

**Computational resources** (when applicable):
- compute scale (GPU hours, cluster time, cloud budget),
- special hardware (FPGA, TPU, quantum),
- engineering infrastructure (distributed training, data pipelines).

**Physical or experimental resources** (when applicable):
- laboratory equipment (microscopes, spectrometers, clean rooms),
- biological or chemical materials,
- animal or human subjects,
- field equipment or field access.

**Data resources** (when applicable):
- dataset scale and origin,
- annotation or labeling effort,
- clinical cohorts or patient registries,
- survey infrastructure,
- archival or library collections.

**Institutional access** (when applicable):
- industry or corporate partnerships,
- clinical or hospital access,
- government or policy access,
- cross-institution coordination.

**Funding clues** (when applicable):
- acknowledged grants or sponsors,
- industry funding,
- national or international grants.

Mark resource claims as **directly stated** or **inferred**.

### Authorship analysis
Use repeated evidence to infer:
- likely students,
- likely postdocs or senior collaborators,
- internal collaborators,
- external academic collaborators,
- industrial or clinical collaborators,
- one-off versus long-term partners.

Do not over-interpret a single author order pattern. Interpret according to the field's authorship norms.

### Impact and signal
State whether the paper appears to be:
- a core paper for the professor,
- a representative student paper,
- a collaboration-heavy paper,
- a transition paper,
- a prestige venue signal,
- a strong indicator of advising or resource access.

### Writing quality
Judge (adapting criteria to the field's scholarly conventions):
- whether the introduction states the problem or research question clearly,
- whether the related work, literature review, or theoretical background builds context well,
- whether the method, argument, or analytical approach is explained clearly,
- whether the evidence (experiments, proofs, data analysis, case studies, textual analysis, clinical data) is rigorous and appropriate for the field,
- whether the paper shows pedagogical clarity,
- (for humanities: quality of prose, sophistication of argument, engagement with primary sources),
- (for biomedical: clarity of clinical significance, appropriate statistical reporting, transparency about limitations and conflicts of interest).

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
- ability to produce influential work (methods, theories, frameworks, discoveries),
- venue consistency (top journals or conferences in the field),
- long-term coherence.

### Mentoring strength
Assess:
- number and stability of probable students (calibrated against the field profile's typical lab structure),
- whether students appear as lead authors (first author in first-and-last fields, or equivalent in other conventions),
- whether students grow over time,
- whether students lead increasingly mature work,
- visible alumni outcomes when available,
- whether the professor seems to create independent researchers.

### Collaboration network
Assess:
- cross-lab, cross-university, cross-country, and industry (or cross-sector) collaborations,
- breadth versus depth,
- repeated high-quality collaborators,
- whether the professor appears central or peripheral in collaborations.

### Resource profile
Assess the resources that matter for this professor's specific field (as identified in the field profile):
- access to the critical resources for their research type (compute, equipment, data, fieldwork access, archival collections, clinical populations, etc.),
- unique or hard-to-replicate resources (proprietary datasets, rare equipment, exclusive partnerships),
- ability to run ambitious projects given available resources,
- efficiency of converting resources into strong outputs.

### Workload and culture risk
Assess cautiously:
- output volume relative to field norms (a professor publishing 30 papers/year in ML may be normal. A professor publishing 30 papers/year in philosophy is a red flag.),
- bursts of many publications in one cycle,
- high throughput patterns,
- fragmentation risk (publishing many thin papers instead of fewer substantial ones),
- signs of mature delegation,
- signs of deadline-driven or pressure-driven culture,
- whether multiple interpretations remain plausible.

Always include at least two plausible explanations for a high-output signal when the evidence is ambiguous.

### Teaching and communication signal
Assess from writing and exposition:
- introduction clarity,
- literature review or related-work organization,
- method or argument explanation,
- figure, table, or proof pedagogy,
- whether the papers appear suitable for training newcomers.

## Step 6. Infer Future Directions and Openings

Use the following signals:
- future-work statements,
- research shifts in the last two to three years,
- new coauthor patterns,
- new datasets, methods, or systems,
- repeated unresolved bottlenecks,
- repeated methods or application patterns,
- new grants or funded projects (when visible).

Answer:
- where the professor is most likely to expand,
- where new students or collaborators are most likely needed,
- which directions are durable,
- which directions may be opportunistic rather than strategic.

## Step 7. Fit Analysis for the Applicant

First, calibrate all advice to the applicant's level **and field** using the Applicant-Level Calibration section above.

Then map the applicant to one or more of these universal research roles. Use the field-appropriate examples to guide mapping. For undergraduate and early master's students, it is acceptable to map them as "learning" a role rather than fully occupying one.

- **empirical researcher / experimentalist**: drives data collection, experiments, or computational studies
  - CS/ML: runs large-scale experiments; biology: designs and executes wet-lab or field experiments; psychology: conducts behavioral studies; clinical medicine: designs and conducts clinical trials or observational studies; public health: conducts epidemiological investigations
- **theory builder**: develops formal frameworks, proofs, or mathematical models
  - math: proves theorems; economics: builds equilibrium models; theoretical CS: analyzes algorithms; philosophy: constructs sustained arguments; literary theory: develops interpretive frameworks
- **interpretive scholar**: produces original readings, critiques, or reinterpretations of texts, artifacts, events, or cultural phenomena
  - literary studies: close reading, comparative literature; history: archival interpretation, historiography; art history: visual analysis; anthropology: ethnographic interpretation; religious studies: textual exegesis
- **clinical / translational researcher**: bridges basic science and patient care, or evaluates interventions in clinical settings
  - medicine: clinical trials, translational research; nursing: evidence-based practice research; pharmacy: drug interaction studies; rehabilitation sciences: intervention evaluation
- **qualitative researcher**: conducts interviews, ethnography, discourse analysis, or other qualitative inquiry
  - sociology: ethnography, grounded theory; education: classroom observation, interview studies; anthropology: participant observation; communication studies: discourse analysis; nursing: patient experience research
- **methodologist**: creates new tools, techniques, protocols, or instruments
  - CS/ML: designs architectures, training procedures; chemistry: develops synthesis methods; sociology: creates survey instruments; clinical medicine: develops diagnostic protocols; digital humanities: builds computational analysis tools
- **resource creator**: builds datasets, benchmarks, corpora, toolkits, or infrastructure
  - CS/ML: benchmark/dataset builder; genomics: sequencing pipelines; digital humanities: annotated corpora; clinical: patient registries, biobanks; history: digitized archives
- **cross-domain bridge**: connects methods or insights from one field to another
  - all fields: someone who brings computational skills to biology, linguistic theory to NLP, statistical methods to humanities, clinical perspective to basic science, etc.
- **application specialist**: applies existing methods to specific domains or problems
  - CS/ML: deploys models in healthcare; engineering: applies theory to product design; public health: applies epidemiological methods to new populations
- **apprentice learner** (for undergraduates and early master's students): someone who brings foundational skills and enthusiasm but is primarily looking to learn research methodology under guidance
  - all fields: a student with coursework knowledge and foundational skills (technical, analytical, or interpretive), eager to gain hands-on research experience

Then judge:
- why this professor is a good fit **for this applicant's level and goals**,
- why this professor may be a risky fit,
- how hard it may be to join (considering the applicant's level — some professors only take PhD students, some welcome undergraduates),
- what the applicant should emphasize,
- what gaps the applicant should fix before reaching out.

### Level-specific fit considerations

**For PhD applicants**: Focus on long-term research alignment, advisor working style, publication trajectory, and career development.
- *Humanities/social sciences*: Also consider theoretical alignment, writing mentorship quality, and whether the professor supports students in developing an independent scholarly voice.
- *Biomedical*: Also consider lab resources, clinical access, funding stability, and whether students get authorship on substantial papers.

**For master's students**: Focus on topic accessibility, project scoping, thesis timeline fit, and whether the professor has successfully advised master's theses. Ask: is there a well-defined sub-problem the student can tackle in 1-2 years?
- *Humanities/social sciences*: A master's thesis may be a critical essay, archival study, or ethnographic report. Does the professor guide students in framing manageable interpretive or analytical questions?
- *Biomedical*: A master's thesis may be a well-bounded experiment, a clinical data analysis, or a systematic review. Does the professor have projects with clear, achievable endpoints?

**For undergraduate researchers (capstone/thesis/專題)**: Focus on entry-point accessibility, learning opportunity, and whether the professor or their senior students have bandwidth to mentor. Ask: is there a task the student can contribute to with their current skills while learning new ones? Does the professor's group have a history of involving undergraduates?
- *Humanities/social sciences*: Undergraduates can assist with literature reviews, archival cataloging, translation, transcription, coding qualitative data, or conducting supervised interviews. Look for professors who value these contributions.
- *Biomedical*: Undergraduates can assist with benchwork, data entry, literature searches, simple analyses, or protocol preparation. Look for professors who have structured onboarding for undergraduates in the lab.

If the applicant background is missing, give conditional advice by applicant type and level instead of generic praise.

### Professor-student type matching

Evaluate what TYPE of student is most likely to thrive under this professor:

- **free explorer** who generates own questions vs. **structured-problem student** who needs clear direction,
- **methodologist** who builds tools vs. **problem-driven** who wants to answer specific questions,
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
- Few or no student lead-author papers in recent years (in fields where students are expected to lead papers).
- No visible growth trajectory for current students (students never progress from middle author to lead author).
- No visible alumni outcomes, or alumni have left the field without clear career paths.
- In small-group fields (humanities, math): no visible student completions or excessively long time-to-degree.

### Level-specific warning signs
- **For undergraduates**: The professor has never worked with undergraduates (no undergraduate co-authors, no mentions of undergraduate mentoring). This is not necessarily blocking but raises the question of whether they have the patience or systems for undergraduate-level guidance.
- **For master's students**: The professor's projects all require multi-year investment with no well-scoped sub-problems. The master's student may struggle to complete meaningful work within 1-2 years.
- **For all levels**: The professor's group is so large that individual mentoring time may be very limited, or so small that there are no peers to learn from.

### Field-specific warning signs
- **Humanities/social sciences**:
  - The professor publishes solely through solo-authored works and shows no pattern of involving students in any visible scholarly output (not even acknowledgments). This may be normal for the field, but for a student seeking mentorship, it raises questions about how involved the professor will be.
  - Students in the group take excessively long to complete degrees (even by humanities standards, where 6-8 years for a PhD is common).
  - The professor's theoretical framework or school of thought is narrow enough that students may have limited career options outside that niche.
  - The professor has no visible engagement with the broader scholarly community (no conference presentations, no editorial boards, no professional service) — this limits the student's network-building opportunities.
- **Biomedical sciences**:
  - The professor's recent publications show no student first-authors — all publications are led by postdocs or the professor themselves. This may mean students are not given substantive project ownership.
  - The lab depends on a single grant that appears close to ending (check grant end dates on NIH Reporter, MOST, etc.).
  - The professor's clinical load appears very heavy (many clinical publications, listed in clinical directories) — they may have limited time for research mentoring.
  - The research requires specialized equipment or patient populations that the professor accesses through a collaboration that may be fragile.
  - The professor publishes many case reports or clinical observations rather than hypothesis-driven research — this is not inherently bad but shapes the type of training a student will receive.
  - IRB/ethics approval for human subjects research can introduce long delays. If the professor's work requires new IRB protocols, the student's timeline may be affected.

### Collaboration dependency
- The professor's recent high-impact work depends heavily on one specific external collaborator or institution.
- Risk: if that collaboration ends, the research line may stall, leaving current students stranded.

### Lab dynamics signals
- Very high student turnover inferred from rapidly changing author lists (in fields where lab-based collaboration is the norm).
- Single-student lab with no visible peer cohort (in fields where group work is expected).
- Publication patterns suggesting fragmentation: many very similar papers with minimal incremental contribution, published in close succession. (Calibrate against field norms. In biomedicine, separate papers for each cohort may be standard practice. In ML, incremental variants of the same method submitted to multiple venues may indicate slicing.)

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
- vague statements like "I am interested in your research",
- copying paper summaries into the email,
- asking for admission without showing fit.

Produce versions appropriate to the applicant's level when the user requests outreach support:
- **PhD applicant email**: demonstrate research maturity and concrete contribution potential.
- **Master's thesis student email**: show specific topic interest, relevant coursework or projects, and willingness to learn.
- **Undergraduate research student email**: show enthusiasm, relevant coursework, specific skills, and concrete knowledge of the professor's research area. Be honest about being an undergraduate — professors appreciate directness.
  - *Humanities/social sciences skills to mention*: language proficiency, close-reading experience, archival research experience, qualitative methods coursework, writing ability, familiarity with specific theoretical frameworks or historical periods.
  - *Biomedical skills to mention*: lab course experience, specific techniques learned (PCR, cell culture, microscopy, etc.), statistics or bioinformatics coursework, clinical shadowing or volunteer experience, familiarity with specific model organisms or disease areas.
  - *STEM/engineering skills to mention*: programming languages, mathematical background, hardware experience, data analysis tools.
- **Research collaboration email** (for postdocs, faculty, or industry researchers).
- **Short relationship-building email** (for initial contact at any level).

For undergraduate and master's students, the tone should be respectful and eager but not groveling. Show that you have done your homework. One paragraph about why their research interests you (with specifics), one paragraph about what you bring, one sentence asking if they have openings or projects suitable for your level.

## Step 9. Conversation and Interview Playbook

Calibrate this section to the applicant's level.

When the user requests meeting preparation, include:
- likely questions from the professor (calibrated to the applicant's level),
- what each question is testing,
- strong answer structure,
- failure modes,
- one or two smart questions the applicant should ask,
- how to pitch a small research idea without sounding naive or arrogant.

### Level-specific preparation

**PhD applicants**: Prepare to discuss research methodology, your publication experience (if any), long-term research interests, and why this specific advisor. Professors are evaluating whether you can become an independent researcher.
- *Humanities/social sciences*: Be ready to discuss the theoretical traditions you are drawn to, your writing sample (if applicable), and how your intellectual interests connect to the professor's work.
- *Biomedical*: Be ready to discuss lab experience, experimental techniques you know, and your understanding of the professor's research questions at a mechanistic level.

**Master's students**: Prepare to discuss relevant coursework, any project experience, and why you want to do thesis research (vs. coursework-only). Professors are evaluating whether you can complete a thesis and whether the topic alignment is workable.
- *Humanities/social sciences*: Be ready to discuss the texts, periods, or phenomena you are interested in, and any preliminary ideas for a thesis topic.
- *Biomedical*: Be ready to discuss relevant lab courses, any research experience, and whether you are interested in experimental vs. computational vs. clinical research.

**Undergraduate researchers (capstone/thesis/專題)**: Prepare to discuss relevant courses, skills (field-appropriate: programming, lab techniques, language abilities, analytical tools, close-reading experience, qualitative methods, etc.), and what you hope to learn. Professors are evaluating whether you have enough foundation to benefit from the experience and whether you are reliable and motivated. Being honest about what you don't know yet is a strength, not a weakness. Show that you've read at least one of their papers or project descriptions and can articulate what interested you.
- *Humanities/social sciences*: Mention relevant courses (theory, methods, area studies), any writing or research you've done, language skills, and what aspect of the professor's work you find intellectually compelling.
- *Biomedical*: Mention relevant lab courses, any techniques you've learned, statistics or computing skills, and what aspect of the professor's research you want to understand better.

### Counter-questioning strategy
Provide questions the applicant can ask to probe:
- mentoring style: "What does a typical first-year project look like?" / "How do students choose topics?"
- lab/group culture: "What does a typical week look like for your students?" / "How does the group handle major publication deadlines or milestones?"
- actual availability: "How often do you meet with students one-on-one?" / "Do students collaborate with each other?"

For undergraduate students, add:
- "Do you currently have undergraduate students in your group?"
- "Is there a specific project that might be suitable for an undergraduate?"
- "Would I work directly with you, or with a graduate student?"
- "What background or skills would help me prepare before starting?"

Frame these so the applicant sounds curious, not interrogating.

### Building match feeling in a short meeting
Structure a 20-minute conversation:
1. (2 min) Open with a specific observation about their recent work — not flattery, but genuine insight or question.
2. (5 min) Connect your background — one project, one skill, one link to their research.
3. (5 min) Float a small research angle you have been thinking about (for PhD applicants) or ask about a specific project you could join (for master's/undergraduate students).
4. (5 min) Ask for the professor's perspective — "Where do you see this heading?" / "What is the bottleneck?"
5. (3 min) Close with practical next steps — "Would it help if I read X before we talk again?" / "Is there a specific preparation I should do?"

### Research idea pitch calibration
- The idea should be small enough to be feasible as a starter project.
- It should connect to the professor's existing line but add a twist from your own background.
- Frame it as "I have been thinking about X and would love your perspective" — not "I want to do X in your lab."
- Prepare for the professor to redirect or dismiss it. That is also valuable information about how they engage with new ideas.
- Avoid ideas that are too ambitious (signals naivety) or too incremental (signals lack of vision).
- **For undergraduates**: It is perfectly fine NOT to pitch a research idea. Instead, express interest in an existing project and ask how you could contribute. Professors often prefer to assign undergraduates to existing projects rather than have them propose new ones.

## Output Contract

Use the template in [references/output-template.md](references/output-template.md).

At minimum, include these sections when enough evidence exists:

1. Field Profile (from Step 0)
2. Professor Snapshot
3. Research Timeline
4. Research Taxonomy
5. Paper-by-Paper Analysis
6. Advisor Assessment
7. Future Directions
8. Fit Analysis for the Applicant
9. Warning Signs
10. Cold Email Templates
11. Conversation and Interview Playbook
12. Final Verdict

If some sections cannot be completed, keep the section title and explicitly state what is missing.

## Final Verdict Requirements

End with:
- what type of applicant **at the user's level** is most likely to thrive with this professor,
- what type is least likely to thrive,
- the strongest opportunity **for the user's specific level**,
- the biggest risk,
- the next three actions the user should take (calibrated to their level — e.g., for undergraduates: "take course X", "learn tool Y", "read paper Z"; for PhD applicants: "prepare research proposal on topic X", "contact current student Y", etc.).

## Guardrails

- Do not present speculation as fact.
- Do not infer workload, personality, or ethics from a single paper.
- Do not assume all recurring coauthors are students.
- Do not assume that all last-author papers are fully driven by the professor.
- Do not apply CS/ML norms to non-CS/ML fields without adjustment.
- Do not apply STEM norms to humanities or social sciences. Solo authorship, low publication rates, book-length works, and theoretical (non-empirical) contributions are all legitimate and prestigious in their fields.
- Do not apply bench-science norms to clinical, public health, or population-based research. Different study designs have different timelines, authorship patterns, and resource requirements.
- Do not penalize low publication volume in fields where it is normal.
- Do not penalize solo authorship in fields where it is standard.
- Do not penalize the absence of a large lab in fields where small groups or solo work is the norm.
- Do not penalize the absence of computational skills in fields where they are not central.
- Do not penalize the absence of laboratory skills in fields that are archival, interpretive, or theoretical.
- Do not hide access limits or incomplete coverage.
- Do not fabricate alumni outcomes.
- Do not optimize for praise. Optimize for decision usefulness.
- Do not assume that "research" means experimental or quantitative work. Interpretive, critical, archival, and creative scholarship are equally valid forms of research.

## References

- [references/evidence-rubric.md](references/evidence-rubric.md). Evidence ladder, confidence rules, and counter-evidence protocol.
- [references/output-template.md](references/output-template.md). Default report structure.
- [references/outreach-playbook.md](references/outreach-playbook.md). Email and interview strategy rules.
