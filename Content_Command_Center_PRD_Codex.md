# CONTENT COMMAND CENTER
## Product Requirements Document (PRD) + Codex Build Specification

**Working name:** Content Command Center  
**Product type:** AI Content Production OS  
**Primary user:** Creator / AI consultant / small content team / client-content operator  
**Primary use case:** Turn research, trends, brand knowledge, design instructions, references, and previous work into ready-to-publish multi-format content with AI agents, while preserving traceability, brand consistency, reusable knowledge, and human approval.

---

# 0. PRODUCT THESIS

Content Command Center is **not** another content calendar and **not** a generic AI chat wrapper.

It is an **AI Content Production Operating System** that remembers:

- Brand
- Project
- Audience
- Offer
- Funnel strategy
- Design instructions
- Motion instructions
- Character / mascot rules
- Prompt versions
- Research and evidence
- Existing assets
- Previous content
- Previous performance
- What can be reused
- Which AI model / agent / skill should perform each task

The system should answer three questions continuously:

1. **What should we create next?**
2. **How should it be created for this specific brand/project?**
3. **What should happen after it is published?**

Core loop:

```text
DISCOVER
→ RESEARCH
→ DECIDE
→ CREATE
→ PRODUCE
→ REVIEW
→ DISTRIBUTE
→ LEARN
→ REUSE
```

The system must avoid restarting from zero every time.

Before creating anything new, it should first ask:

> What do we already know, what already exists, and what can be reused or remixed?

---

# 1. PRODUCT GOALS

## 1.1 Primary goals

### G1. Reduce repeated work
Reuse research, hooks, visual patterns, prompts, assets, design rules, scripts, screenshots, references, and previous content.

### G2. Preserve brand consistency
Every generation should inherit the correct design system, project context, audience, offer, funnel, visual rules, and do/don't constraints.

### G3. Connect research directly to production
Research should not end as notes. It should become ideas, scripts, visuals, campaigns, and measurable content.

### G4. Support AI-native content production
The system should support:
- text
- image
- carousel
- infographic
- motion planning
- video planning
- voiceover text
- subtitles
- production packs

### G5. Use specialist agents
Different tasks should be handled by specialist agents / skills rather than one general chatbot.

### G6. Maintain human control
Important stages should support approval checkpoints and manual override.

### G7. Trace everything
Every output should have a lineage:
- source research
- prompt version
- design version
- agent
- model
- tool
- generated asset
- human approval
- final published result

### G8. Learn from performance
The system should recommend follow-up content based on actual performance, not generic AI suggestions.

---

# 2. NON-GOALS

For MVP, do **not** build:

- Full Canva replacement
- Full social scheduling platform replacement
- Full video editor
- Full browser automation framework from scratch
- Full CRM
- Fully autonomous publishing without approval
- Heavy enterprise DAM features
- Multi-tenant billing engine
- Complex agency white-labeling

Instead, build the **brain + production layer** and integrate external tools where appropriate.

---

# 3. PRODUCT PRINCIPLES

## P1. Context before generation
No important generation should start from an empty prompt.

## P2. Search before create
Check existing content, research, prompts, assets, and references first.

## P3. Project-specific rules override global rules
Resolution order:

```text
1. Current task explicit instructions
2. Campaign instructions
3. Project-specific instructions
4. Brand design instructions
5. Global design instructions
6. AI defaults
```

## P4. Agents are not prompts
An agent consists of:

```text
Agent =
Role
+ Context
+ Skills
+ Tools
+ Permissions
+ Model
+ Output schema
```

## P5. Human approval is first-class
Approval gates are part of the workflow, not an afterthought.

## P6. Everything important is versioned
Prompts, design systems, content, research claims, and production outputs should have version history.

## P7. Performance must influence future production
Analytics should change what the system recommends next.

---

# 4. TARGET USERS

## Persona A: Creator / AI Educator
Needs:
- trend discovery
- fast scripts
- visual creation
- carousel generation
- consistent personal brand
- repurposing
- performance-based next ideas

## Persona B: AI Consultant
Needs:
- multiple client/project contexts
- project-specific design systems
- research-backed content
- reusable prompts
- client approval
- exportable production packs

## Persona C: Small Content Team
Needs:
- role-based workflow
- review queues
- shared asset library
- execution history
- approvals
- project separation

## Persona D: Client Viewer
Needs:
- see drafts
- view visuals
- comment
- approve / request change
- see calendar
- see performance

Client Viewer should not see internal prompts, costs, run history, or system logic.

---

# 5. INFORMATION ARCHITECTURE

Main navigation:

```text
HOME

DISCOVER
  Trends
  Research
  Ideas

CREATE
  Content
  Visual Studio
  Video / Motion

PLAN
  Calendar
  Campaigns
  Funnel

LIBRARY
  Assets
  References
  Prompts
  Design Systems
  Characters
  Skills

PERFORMANCE
  Analytics
  Comments
  Winning Patterns

SYSTEM
  Brands
  Projects
  Agents
  Integrations
  Runs
  Usage
  Settings
```

---

# 6. HOME / TODAY DASHBOARD

Purpose:
Tell the user what needs attention next.

## 6.1 Widgets

### A. Today
Show:
- items due today
- drafts awaiting review
- missing visuals
- overdue approvals
- pending fact checks
- unpublished ready content

### B. Recommended Next Action
Example:

```text
Claude motion graphics is trending.
You already have:
✓ research
✓ 2 references
✓ previous Claude screenshots
✓ motion style

Estimated time: 15 minutes

[Continue]
```

### C. Funnel Gap
Example:

```text
Last 7 days

TOF  6
MOF  3
BOF  0

Recommendation:
Convert "Claude Motion Graphics" into a BOF workshop post.
```

### D. Reuse Opportunities
Example:

```text
You already have 7 reusable assets related to AI Agents.
[Review reuse options]
```

### E. Agent activity
Show:
- running
- waiting
- failed
- awaiting approval

---

# 7. PROJECT BRAIN

Every content item must belong to a project.

## 7.1 Project fields

```text
Project Name
Brand
Project Goal
Audience
Offers
Primary Funnel
Secondary Funnels
Platforms
Brand Voice
Design System
Motion System
Character Set
Content Pillars
Preferred CTA
Forbidden Claims
Reference Collections
Knowledge Sources
Project Notes
Project Status
```

## 7.2 Example

```text
Project: modty.ai

Goal:
Educate Thai beginners about practical AI and convert interest into workshops / consulting / digital products.

Audience:
AI beginners
Creators
Business owners
People building AI workflows

Content Pillars:
AI Product
Automation
Creator Tools
Vibe Coding
Business Systems

Design System:
modty-design-v1.0
```

---

# 8. CONTEXT STACK

Every major generation should assemble a context stack.

```text
GLOBAL
↓
USER WORKING STYLE
↓
BRAND
↓
PROJECT
↓
CAMPAIGN
↓
CONTENT
↓
FORMAT
↓
REFERENCE
↓
CURRENT REQUEST
```

## 8.1 Context resolver

Create a backend service:

```text
resolveContext(taskId)
```

Output:

```json
{
  "global_rules": [],
  "brand_context": {},
  "project_context": {},
  "campaign_context": {},
  "design_system": {},
  "motion_system": {},
  "content_context": {},
  "references": [],
  "current_instruction": {}
}
```

---

# 9. DESIGN SYSTEM MEMORY

This is a core differentiator.

Design system should be stored as structured data plus Markdown.

## 9.1 Recommended files

```text
/design-systems
  /modty-ai
    brand.md
    design.md
    typography.md
    components.md
    image-style.md
    motion-style.md
    carousel.md
    tiktok-cover.md
    infographic.md
    do-not.md
```

## 9.2 Required design sections

### Brand Direction
- personality
- visual feeling
- visual boundaries

### Color System
- primary
- secondary
- background
- text
- accent
- color rules

### Typography
- heading fonts
- body fonts
- English fonts
- weight
- hierarchy
- mobile readability rules

### Layout
- preferred layouts
- spacing
- safe margins
- negative space
- hierarchy

### Shapes
- rounded rectangles
- circles
- ovals
- curved frames
- decorative lines

### Card Style
- standard
- neo-brutalist
- soft
- premium
- dark

### Image Style
- preferred
- forbidden
- people rules
- product rules
- screenshots
- 3D objects

### Motion Style
- transitions
- entry animation
- emphasis
- camera movement
- timing
- easing
- motion trails
- curved paths

### Format Presets
- TikTok cover
- carousel
- infographic
- B-roll graphic
- thumbnail
- story

### Do / Don't
Explicit rules.

---

# 10. DESIGN INSTRUCTION RESOLUTION

When generating an output:

```text
TASK
+
CONTENT CONTEXT
+
PROJECT CONTEXT
+
BRAND DESIGN
+
PROJECT DESIGN OVERRIDE
+
FORMAT PRESET
+
REFERENCE DNA
+
CURRENT USER INSTRUCTION
=
FINAL VISUAL INSTRUCTION
```

If conflict exists:

```text
Current task > Campaign > Project > Brand > Global > Model default
```

---

# 11. DESIGN INSTRUCTION EXTRACTOR

Input:
- image
- screenshot
- carousel
- website
- poster
- video
- brand guideline

Output:

```text
Colors
Typography
Spacing
Shapes
Layout
Hierarchy
Image style
Component style
Motion style
Do / Don't
Reference DNA
```

Actions:
- Save as design system
- Save as project override
- Save as reference only
- Compare with existing design system

---

# 12. REFERENCE DNA

Do not treat a reference as one indivisible style.

Extract independent dimensions:

```text
Composition DNA
Layout DNA
Typography DNA
Spacing DNA
Color DNA
Image DNA
Motion DNA
Camera DNA
Transition DNA
Information Hierarchy
```

User should be able to apply only selected DNA:

```text
[✓] Composition
[ ] Color
[✓] Motion
[ ] Typography
[✓] Camera
```

This supports:
"Use the movement and composition, but not their color/style."

---

# 13. DISCOVER MODULE

## 13.1 Trend Radar

Sources:
- AI product updates
- creator tools
- GitHub
- social trends
- viral topics
- community discussions
- user comments
- internal performance signals

Trend object:

```text
Title
Source
URL
Detected At
Category
Trend Score
Relevance Score
Audience Fit
Project Fit
Funnel Fit
Why It Matters
Potential Angles
Freshness
Status
```

## 13.2 Trend categories

```text
AI Trend
Social Trend
Wild Trend
Product Update
Open-source
Creator Trend
Business Trend
```

## 13.3 Trend scoring

Possible weighted score:

```text
trend_score =
freshness * 0.25
+ velocity * 0.20
+ project_fit * 0.20
+ audience_fit * 0.20
+ content_potential * 0.15
```

Do not expose a meaningless score without explanation.

---

# 14. RESEARCH VAULT

Research must be structured and reusable.

## 14.1 Research Item

```text
Topic
Research Question
Summary
Source URL
Source Type
Published Date
Claim
Evidence
Confidence
Last Verified
Freshness
Used In Content
Tags
```

## 14.2 Claim status

```text
Fresh
Needs Verify
Outdated
Conflicting
Unsupported
```

## 14.3 Research actions

- Save
- Verify
- Compare
- Attach to content
- Convert to idea
- Convert to script
- Mark outdated

---

# 15. FACT QA AGENT

Before publish, check all factual claims.

Example:

```text
CLAIM
"Tool X is available in Thailand."

STATUS
Needs verification

SOURCE
Official product documentation

LAST CHECKED
2026-10-07
```

Rules:
- High-risk factual claims must be sourced.
- Time-sensitive product claims should have verification date.
- Failed fact checks can block publish.

---

# 16. IDEA BANK

Statuses:

```text
Raw
Shortlisted
Selected
Scripted
Producing
Ready
Published
Repurpose
Archived
```

Idea fields:

```text
Title
Description
Source
Trend
Research
Project
Audience
Funnel
Content Pillar
Offer
Format
Priority
Potential Score
Hook Candidates
Status
```

Actions:
- Develop
- Convert to content
- Merge ideas
- Duplicate
- Archive
- Add to campaign

---

# 17. FUNNEL SYSTEM

Supported funnels:

```text
TOF
MOF
BOF
```

Each content item must have a funnel assignment.

Dashboard should show:

```text
TOF  62%
MOF  28%
BOF  10%
```

System should detect gaps and recommend content to fill them.

Example:
"Too much TOF. Convert your AI Motion post into a BOF workshop post."

---

# 18. OFFER MAPPING

Every content item may map to an offer.

Offer object:

```text
Offer Name
Offer Type
Price
Audience
Problem
Outcome
CTA Templates
Related Content Pillars
Related Funnel Stages
Active / Inactive
```

Example mapping:

```text
Content:
Claude Motion Graphics

Relevant Offer:
AI Video Creation Workshop

Suggested CTA:
Comment "MOTION"
```

---

# 19. CTA LIBRARY

CTA categories:

```text
Engagement
Comment
Save
Share
Lead
DM
Product
Workshop
Soft CTA
Part 2
Newsletter
Consulting
```

Each CTA should track:
- usage count
- content types
- average performance
- best funnel
- best platform

---

# 20. HOOK LIBRARY

Store **patterns**, not only final text.

Example:

```text
Pattern:
"Don't start from zero"

Works best for:
Open-source
Tutorial
Tools

Example:
"9 GitHub repos that mean you don't need to start from zero"
```

Performance fields:
- average hold rate
- saves
- shares
- comments
- CTR

---

# 21. CONTENT BUILDER

Main workspace for content creation.

## 21.1 Inputs

```text
Project
Idea
Research
Audience
Platform
Funnel
Offer
Format
Goal
Tone
Reference
```

## 21.2 Outputs

```text
Hook
Script
Caption
CTA
Title
Description
Hashtags
Visual Plan
Shot List
Carousel Structure
Image Briefs
Video Brief
Voiceover
SRT Draft
```

## 21.3 Script structure

For short video:

```text
0-3s Hook
3-15s Problem
15-35s Demo / Explanation
35-45s Result
45-60s CTA
```

Editable, not fixed.

---

# 22. VISUAL DIRECTOR

The Visual Director should read the script and decide which visuals are required.

Example:

```text
Content length: 47 seconds
Recommended visual count: 8

1 Hook Graphic
2 Product Screenshot
3 UI Animation Frame
4 Comparison Graphic
5 Demo Screen
6 Result Graphic
7 CTA Graphic
8 Thumbnail
```

Actions:
- Approve plan
- Edit visual plan
- Generate all
- Generate selected
- Regenerate one

---

# 23. AI VISUAL STUDIO

## 23.1 Supported output types

```text
Cover
Carousel
Infographic
B-roll graphic
Thumbnail
Product visual
UI mockup
Illustration
3D object
Story
Motion-ready asset
```

## 23.2 Visual generation context

Every image request should automatically include:

```text
Content
Visual Goal
Brand
Design Instructions
Project Override
Format
Reference DNA
Approved Text
Composition
Motion Readiness
Avoid Rules
```

## 23.3 Prompt engine

Internal prompt structure:

```text
ROLE
CONTENT
VISUAL PURPOSE
DESIGN INSTRUCTIONS
PROJECT OVERRIDE
REFERENCE ANALYSIS
FORMAT
TEXT
COMPOSITION
MOTION READINESS
AVOID
```

User does not need to see full prompt by default.

---

# 24. IMAGE MODEL ROUTER

Do not hard-code one model.

Create provider abstraction.

Example:

```text
TASK
Photoreal product
→ Provider A

Typography-heavy visual
→ Provider B

Fast draft
→ Provider C

Image edit
→ Provider D
```

Provider interface:

```ts
interface ImageProvider {
  generate(input: ImageGenerationInput): Promise<ImageGenerationResult>
  edit?(input: ImageEditInput): Promise<ImageGenerationResult>
}
```

---

# 25. CAROUSEL GENERATOR

Input:
- content
- design system
- slide count
- platform
- reference

Output:
- slide structure
- copy per slide
- visual brief per slide
- generated image per slide

Example grid:

```text
01 ✓
02 ✓
03 ✓
04 Regenerate
05 ✓
06 ✓
```

Regenerate individual slides without rerunning the entire set.

---

# 26. FORMAT ADAPTATION

From one approved master visual:

```text
TikTok Cover 9:16
Instagram Feed 4:5
Square 1:1
YouTube Thumbnail 16:9
Story 9:16
```

Important:
Do not just crop.
Re-layout elements based on safe areas and hierarchy.

---

# 27. QUICK IMAGE EDITOR

Quick commands:

```text
Change background
Add text space
Remove person
Apply brand colors
Make product clearer
Convert to 9:16
Add mascot
Make 3D
Reduce clutter
Increase contrast
Create transparent asset
```

All edits should preserve lineage to source image.

---

# 28. ASSET LIBRARY

Asset types:

```text
Image
Video
Screenshot
Logo
Mascot
Character
Audio
Voice
Reference
Template
Prompt
Motion asset
UI
Document
```

Asset fields:

```text
Name
Type
Project
Brand
Tags
Source
Created By
Created At
Used In
Design Version
Prompt Version
Model
License / Rights Note
Status
```

Actions:
- Reuse
- Edit
- Adapt
- Duplicate
- Archive
- Attach to project
- Attach to content

---

# 29. REUSE ENGINE

Before generating new content or assets:

```text
Search:
Research
Previous script
Screenshot
Image
Prompt
Carousel
Video
Design
Reference
Hook
CTA
```

Then show:

```text
7 reusable items found

[Reuse]
[Update]
[Remix]
[Generate New]
```

This should run automatically.

---

# 30. CHARACTER / MASCOT BIBLE

Character object:

```text
Name
Identity
Face
Body
Hair
Wardrobe
Personality
Expressions
Voice
Camera Preference
Do Not Change
Reference Images
Color Rules
Allowed Poses
Forbidden Changes
```

All generated character assets should reference Character ID and version.

---

# 31. MOTION SYSTEM

Store reusable motion vocabulary.

Example:

```text
ENTRY
Scale 90 → 100
0.6s

CARD
Slide + overshoot

TEXT
Mask reveal

EMPHASIS
Circle draw

TRANSITION
Curved wipe

CAMERA
Slow push-in
```

Motion system should include:
- timing
- easing
- entry
- exit
- emphasis
- camera
- transition
- path
- layer behavior

---

# 32. MOTION-READY IMAGE GENERATION

Mode:

```text
Static
Motion-ready
```

Motion-ready output should consider:

```text
Background
Midground
Foreground
Isolated objects
Transparent elements
Text-safe area
Layer separation
Parallax potential
Suggested animation
```

---

# 33. VIDEO / MOTION MODULE

MVP does not need full editing.

Outputs:
- storyboard
- shot list
- motion instructions
- asset list
- voiceover
- SRT
- production pack

Future:
- HTML motion
- Remotion
- HyperFrames
- render workflow
- video model integration

---

# 34. ONE-CLICK PRODUCTION PACK

Export:

```text
/script.md
/caption.txt
/shot-list.md
/image-prompts.md
/video-prompts.md
/assets/
/references/
/voiceover.txt
/subtitles.srt
/design-context.md
/research-sources.md
```

Optional:
ZIP download.

---

# 35. CONTENT CALENDAR

Calendar should not be just date cards.

Each card shows:

```text
Title
Project
Platform
Funnel
Status
Script
Visual
Approval
Publish status
```

Color by funnel:

```text
TOF
MOF
BOF
```

Capabilities:
- drag and drop
- filter by project
- filter by platform
- filter by funnel
- filter by status
- batch move
- campaign view

---

# 36. PUBLISH QUEUE

States:

```text
Draft
Ready for Review
Approved
Ready to Publish
Scheduled
Published
Failed
```

MVP:
Prepare final package and export.

Later:
Connect to external publisher / social APIs.

---

# 37. PERFORMANCE MODULE

Metrics:

```text
Views
Likes
Comments
Shares
Saves
Watch Time
Completion Rate
CTR
Leads
Conversions
Revenue attribution
```

AI analysis:

```text
Why it worked
What failed
What to repeat
What to change
Best hook pattern
Best visual pattern
Best CTA
Best funnel fit
Recommended next move
```

Recommended next move:

```text
Follow-up
Part 2
Deep Dive
BOF Version
Remix
Stop
```

---

# 38. COMMENT MINING

Classify comments:

```text
Question
Objection
Pain Point
Request
Confusion
Buying Intent
Content Idea
FAQ
```

Example:

```text
Comment:
"คนไทยใช้ได้หรือยัง"

Converted idea:
"AI Agents ตัวไหนใช้ในไทยแล้วบ้าง"
```

---

# 39. AUDIENCE QUESTIONS DATABASE

Aggregate repeated questions.

Example:

```text
"ใช้ฟรีไหม" asked 28 times
```

Recommendations:
- create content
- add FAQ
- update product page
- create comparison post

---

# 40. CONTENT LINEAGE

Every content object should expose:

```text
Trend
↓
Research
↓
Idea
↓
Script
↓
Visual
↓
Published Post
↓
Performance
↓
Repurpose
```

Store links between entities.

This enables:
- provenance
- debugging
- learning
- reuse
- auditing

---

# 41. VERSION HISTORY

Version:
- design system
- prompt
- content
- script
- asset
- research claim
- character
- motion system

Example:

```text
modty-design-v1.0
modty-design-v1.1
modty-design-v1.2
```

Every generated asset stores which version was used.

---

# 42. PROMPT REGISTRY

Prompt object:

```text
Name
Slug
Version
Purpose
Input Schema
Prompt Body
Output Schema
Used By
Last Changed
Created By
Performance
Status
```

Examples:

```text
carousel-generator v3.4
image-director v2.1
motion-analysis v5.0
research-synthesizer v1.2
```

Capabilities:
- rollback
- clone
- test
- compare
- activate version

---

# 43. SKILLS LIBRARY

Skills are reusable capabilities.

Examples:

```text
Research latest AI news
Analyze GitHub repo
Generate carousel
Generate TikTok script
Extract design DNA
Create motion storyboard
Fact check availability
Generate SRT
Repurpose content
Create CTA
Search existing assets
```

Skill object:

```text
Name
Description
Inputs
Outputs
Tools
Model Preference
Prompt Version
Permissions
Status
```

---

# 44. AGENT ARCHITECTURE

## 44.1 Content Team

```text
01 Trend Scout
02 Researcher
03 Strategist
04 Script Writer
05 Visual Director
06 Image Designer
07 Motion Director
08 Fact Checker
09 Brand Guardian
10 Performance Analyst
```

## 44.2 Operator Agents

```text
Browser Operator
File Operator
App Operator
Publisher
```

## 44.3 Supervisor

User asks:

> "ทำคอนเทนต์เรื่อง Open-source AI Agents"

Supervisor generates:

```text
TASK PLAN

✓ Search existing content
✓ Research latest information
✓ Verify sources
✓ Choose funnel
✓ Write TikTok script
✓ Create 6 visuals
✓ Brand QA
✓ Prepare publishing pack
```

---

# 45. AGENT DEFINITION

Example:

```text
Visual Director

ROLE
Visual strategy

CONTEXT
Brand + Project + Content + Design System

SKILLS
Analyze reference
Choose layout
Build storyboard

TOOLS
Asset Search
Image Generator

MODEL
Visual reasoning model

PERMISSION
Cannot publish

OUTPUT
visual-plan.json
```

---

# 46. OPEN-SOURCE AGENT INSPIRATION

Use these as inspiration or pluggable infrastructure, not mandatory monolithic dependencies.

## Browser automation
- Browser Use pattern

Use for:
- web research
- competitor scan
- screenshots
- extracting page information

## Deep research
- LangChain deep research patterns

Use for:
- question decomposition
- multi-source research
- synthesis
- evidence collection

## AI workspace / operating environment
- Kortix / Suna pattern

Use for:
- file workspace
- persistent project context
- skills
- sandboxed task execution
- human approval

## Multi-agent orchestration
- CrewAI-style crews / flows

Use for:
- specialist roles
- deterministic workflow
- agent handoffs

## General autonomous task planning
- OpenManus pattern

Use for:
- task decomposition
- multi-step execution

## Tool / app actions
- Composio-style integration layer

Use for:
- external apps
- auth
- triggers
- tool calling

## Scheduled / trigger automation
- AutoGPT-like event patterns

Use for:
- recurring jobs
- conditional workflows

Important:
Do not combine all frameworks into the core runtime.
Create internal abstractions so providers/frameworks can be replaced.

---

# 47. HUMAN APPROVAL MODES

Modes:

## Manual
Approve every stage.

```text
Research
→ Approve
Idea
→ Approve
Script
→ Approve
Visual
→ Approve
Final
→ Publish
```

## Assisted
Approve:
- script
- final

## Autopilot
AI continues until:
- ready for publish
- policy block
- factual uncertainty
- missing required input

---

# 48. QA SYSTEM

## 48.1 Fact QA
Check:
- factual claims
- availability
- dates
- feature claims
- price claims
- location claims

## 48.2 Brand QA
Check:
- brand voice
- tone
- banned phrases
- audience fit

## 48.3 Visual QA
Check:
- text readability
- Thai text
- safe margin
- brand colors
- clutter
- hierarchy
- missing logo
- visual mismatch

Example:

```text
Brand compliance: 92%
Text readability: PASS
Thai text accuracy: FAIL
Safe margin: PASS
Too much text: WARNING
```

Action:
`Fix automatically`

---

# 49. QUALITY SCORE

Do not expose one meaningless number.

Show dimensions:

```text
Hook: Strong
Clarity: Good
Novelty: Medium
Proof: Weak
CTA: Missing
Visual Potential: High
Funnel Fit: TOF ✓
```

System should identify the highest-impact issue.

---

# 50. AGENT RUN HISTORY

Every run:

```text
Run ID
Agent
Task
Input
Context
Skills
Tools
Model
Prompt Version
Output
Status
Started At
Finished At
Duration
Cost
Error
Approval
```

UI example:

```text
Trend Scout       DONE
Researcher        DONE
Strategist        DONE
Writer            RUNNING
Visual Director   WAITING
Brand QA          WAITING
```

---

# 51. COST / USAGE TRACKING

Track:

```text
Research
Text AI
Images
Video
Browser
Storage
External APIs
```

Example:

```text
THIS MONTH

Research     $4.20
Text AI      $7.40
Images       $28.60
Video        $61.20

TOTAL        $101.40
```

Also per content item.

---

# 52. CLIENT MODE

Client sees:

```text
Calendar
Draft
Visual
Comment
Approve
Performance
```

Client does not see:
- prompts
- model costs
- agent system prompts
- internal run logs
- debugging
- hidden notes

---

# 53. REPURPOSE GRAPH

From one source:

```text
TikTok
├ Carousel
├ Facebook Post
├ Threads
├ Newsletter
├ Tutorial
├ Workshop Topic
└ Lead Magnet
```

Repurposing must restructure content for each format, not just rewrite.

---

# 54. BATCH PRODUCTION MODE

Example:

```text
Create 5 pieces for next week
```

Workflow:

```text
5 Ideas
→ approval
5 Scripts
→ approval
5 Visual Plans
→ approval
5 Covers
→ Calendar
```

Do not generate an entire expensive batch before checkpoint.

---

# 55. SCHEDULED AUTOMATION CONCEPTS

Examples:

```text
Every day 08:00
→ Trend Scout

If Trend Score > 80
→ Researcher

If Project Fit > threshold
→ Generate Idea

→ Notify user
```

Do not auto-publish in MVP.

---

# 56. DATA MODEL

Recommended database:
PostgreSQL.

Optional:
pgvector for embeddings / semantic retrieval.

## 56.1 Core tables

```text
users
workspaces
workspace_members

brands
projects
campaigns
offers
audiences

design_systems
design_system_versions
motion_systems
motion_system_versions

characters
character_versions

research_items
research_claims
research_sources

trends
ideas
content_items
content_versions

scripts
visual_plans
visual_items
assets
references

prompts
prompt_versions
skills
agents
agent_runs

approval_requests
comments

calendar_entries
publish_jobs

performance_records
content_patterns
hook_patterns
cta_patterns

usage_records
integration_connections
```

---

# 57. IMPORTANT ENTITY RELATIONSHIPS

```text
Workspace
  ├ Brand
  │   ├ Design System
  │   ├ Character
  │   └ Projects
  │       ├ Campaign
  │       ├ Research
  │       ├ Ideas
  │       ├ Content
  │       └ Assets

Content
  ├ Research
  ├ Idea
  ├ Prompt Version
  ├ Design Version
  ├ Visual Plan
  ├ Assets
  ├ Approval
  ├ Publish
  └ Performance
```

---

# 58. RECOMMENDED TECH STACK

## Frontend
- Next.js
- TypeScript
- React
- Tailwind CSS
- shadcn/ui or internal component system

## Backend
- Next.js server actions / route handlers for MVP
or
- separate Node API later

## Database
- PostgreSQL
- Supabase recommended for fast MVP
- pgvector optional

## Authentication
- Supabase Auth or Clerk

## File storage
- Supabase Storage or S3-compatible storage

## Background jobs
Choose one:
- Trigger.dev
- Inngest
- BullMQ + Redis

Recommended MVP:
Trigger.dev or Inngest.

## Realtime
- Supabase Realtime
or
- SSE for agent run updates

## AI provider abstraction
Create internal adapters:
- text model
- image model
- browser tool
- research provider
- embeddings

Do not make business logic depend on one model.

---

# 59. RECOMMENDED APP ARCHITECTURE

```text
/apps
  /web

/packages
  /db
  /ui
  /agents
  /skills
  /ai
  /design-engine
  /research
  /content-engine
  /visual-engine
  /qa
  /integrations
  /shared
```

For a simpler single-repo MVP:

```text
/src
  /app
  /components
  /features
  /lib
    /ai
    /agents
    /skills
    /db
    /design
    /research
    /content
    /visual
    /qa
    /integrations
  /types
```

---

# 60. PROPOSED FEATURE MODULES

```text
/features
  /home
  /projects
  /design-systems
  /research
  /trends
  /ideas
  /content
  /visual-studio
  /calendar
  /library
  /agents
  /performance
  /settings
```

---

# 61. API / SERVICE LAYER

Recommended internal services:

```text
ContextResolver
ReuseEngine
ResearchService
TrendService
ContentService
DesignResolver
PromptResolver
AgentOrchestrator
VisualService
QAService
AssetService
PerformanceService
UsageService
ExportService
```

---

# 62. CORE SERVICE CONTRACTS

## Context Resolver

```ts
resolveContext({
  workspaceId,
  projectId,
  campaignId?,
  contentId?,
  format?,
  currentInstruction?
})
```

## Reuse Engine

```ts
findReusable({
  projectId,
  query,
  types,
  limit
})
```

## Design Resolver

```ts
resolveDesign({
  brandId,
  projectId,
  campaignId?,
  format,
  taskOverrides?
})
```

## Agent Run

```ts
runAgent({
  agentId,
  task,
  context,
  inputs,
  approvalMode
})
```

---

# 63. EVENT MODEL

Suggested domain events:

```text
project.created
research.completed
research.needs_verification
idea.created
idea.approved
content.created
content.approved
visual_plan.created
visual.generated
visual.qa_failed
content.ready_to_publish
content.published
performance.updated
repurpose.recommended
agent.run_started
agent.run_completed
agent.run_failed
approval.requested
approval.completed
```

---

# 64. SEARCH / MEMORY STRATEGY

Use two forms of retrieval:

## Structured filters
For:
- project
- brand
- tags
- type
- status
- date
- funnel
- platform

## Semantic retrieval
For:
- similar research
- similar scripts
- previous ideas
- visual references
- prompts
- comments

Semantic search should augment, not replace, explicit project scoping.

---

# 65. SECURITY / PERMISSIONS

Roles:

```text
Owner
Admin
Editor
Reviewer
Client Viewer
```

Permissions:
- project-level access
- prompt visibility
- cost visibility
- publish permission
- client review permission
- agent configuration permission

Never expose:
- API keys
- hidden system prompts
- internal credentials

---

# 66. LICENSING / OPEN-SOURCE RULE

Before directly embedding any external open-source project:

1. Check current license.
2. Check commercial-use rights.
3. Check hosted-service restrictions.
4. Prefer patterns / abstractions over copying entire codebases.
5. Keep agent framework replaceable.

Create:

```text
/third-party/NOTICE.md
```

Document:
- dependency
- repository
- version
- license
- use in product

---

# 67. MVP SCOPE

Build only the highest-leverage workflow.

## MVP modules

### M1. Workspace / Project Brain
- brands
- projects
- audience
- offers
- content pillars

### M2. Design Systems
- design instruction editor
- versioning
- project override
- format presets

### M3. Research + Idea Inbox
- research items
- source links
- ideas
- convert research → idea

### M4. Content Builder
- hook
- script
- caption
- CTA
- funnel
- platform
- project context

### M5. Visual Studio
- visual plan
- generate image
- use design system
- reference
- asset library
- carousel batch

### M6. Calendar
- status
- funnel
- project
- date

### M7. Prompt + Asset Library
- prompt registry
- asset reuse
- version tracking

### M8. Approval + Run History
- approval
- agent runs
- basic execution logs

---

# 68. MVP OUT OF SCOPE

Do not build initially:

- automatic social publishing
- complete video editor
- complex workflow builder
- team billing
- public marketplace
- browser agent UI
- full analytics ingestion
- comment ingestion
- advanced model router
- autonomous background agent swarm

---

# 69. PHASE 2

Add:

- Trend Radar
- Performance
- Comment Mining
- Repurpose
- Fact QA
- Visual QA
- Funnel analytics
- Hook / CTA pattern analysis
- Design extractor
- content lineage UI

---

# 70. PHASE 3

Add:

- Multi-agent orchestration
- Browser operator
- Research agent
- App operator
- Image/video model router
- Scheduled automation
- Client portal
- Cost tracking
- publisher integrations
- production pack automation
- motion generation / render pipeline

---

# 71. MVP PRIMARY USER FLOW

```text
1. Create Project
2. Add Brand + Audience + Offer
3. Add Design Instructions
4. Add Research / Idea
5. Click "Create Content"
6. System resolves project context
7. System searches reusable items
8. Generate Hook + Script + Caption
9. Approve
10. Generate Visual Plan
11. Generate Cover / Carousel
12. Visual QA
13. Approve
14. Add to Calendar
15. Export Production Pack
```

---

# 72. VISUAL GENERATION FLOW

```text
User selects content
↓
Context Resolver
↓
Reuse Engine
↓
Design Resolver
↓
Reference DNA
↓
Visual Director
↓
Prompt Resolver
↓
Image Provider
↓
Asset Library
↓
Visual QA
↓
Human Approval
```

---

# 73. CONTENT GENERATION FLOW

```text
Idea
↓
Research
↓
Project Brain
↓
Audience
↓
Funnel
↓
Offer
↓
Hook Pattern
↓
Script Generator
↓
Fact QA
↓
Brand QA
↓
Human Approval
```

---

# 74. DATABASE MVP MINIMUM

For first implementation, start with:

```text
users
workspaces
brands
projects
design_systems
research_items
ideas
content_items
assets
prompts
agent_runs
calendar_entries
approval_requests
```

Do not create every future table on day one.

---

# 75. MVP PAGE LIST

```text
/
  Home

/projects
/projects/[id]

/design
/design/[id]

/research

/ideas

/content
/content/[id]

/visual

/calendar

/library

/system/runs
```

---

# 76. UI DESIGN DIRECTION

Default UI direction:

```text
Cream / warm white background
Orange accent
Black text
Rounded cards
Clear hierarchy
Minimal clutter
Kanit for Thai headings
Sarabun or Kanit regular for body
No handwriting fonts
Clean SaaS UI
Light neo-brutalist accents
```

Important:
Product UI and generated content design systems must be separate.
The app can use modty.ai style by default, but project outputs must follow the selected project design system.

---

# 77. HOME SCREEN MOCK STRUCTURE

```text
------------------------------------------------
CONTENT COMMAND CENTER

Project: modty.ai          [Switch Project]
------------------------------------------------

TODAY
3 things need attention

[Trend worth creating]
[3 scripts waiting review]
[1 visual incomplete]

------------------------------------------------

RECOMMENDED NEXT ACTION

Claude Motion Graphics
Research ✓
Reference ✓
Assets ✓

[Continue Production]

------------------------------------------------

FUNNEL GAP

TOF 6
MOF 3
BOF 0

[Create BOF Content]

------------------------------------------------

AGENT ACTIVITY

Researcher     DONE
Writer         RUNNING
Visual         WAITING
------------------------------------------------
```

---

# 78. ACCEPTANCE CRITERIA — MVP

## Project Brain
- User can create project
- User can assign audience
- User can assign offers
- User can attach design system

## Design System
- User can create / edit design instructions
- System supports project override
- Version is stored
- Visual generation records version used

## Research
- User can store URL + summary + claims
- Research can convert to idea

## Content
- User can create script from idea
- Output uses project context
- Output is editable
- Version history is stored

## Visual
- User can create visual plan
- User can generate at least one image
- Generation uses design system
- Asset saved to library
- User can regenerate individual item

## Calendar
- User can schedule content
- Filter by project / funnel / status

## Run History
- Every AI generation creates a run record
- Run stores model/provider, status, timing, prompt version

---

# 79. CODEX IMPLEMENTATION RULES

Codex should follow these rules:

1. Build vertical slices, not all database tables first.
2. Keep provider abstractions from day one.
3. Keep UI functional before adding heavy automation.
4. Every AI generation must create an agent run record.
5. Every generated asset must store lineage metadata.
6. Project context must be mandatory for generation.
7. Never hard-code brand rules into prompts.
8. Store design instructions separately.
9. Reuse Engine should exist before broad batch generation.
10. Human approval must be supported before auto-publish.
11. Use typed schemas for all AI outputs.
12. Validate AI JSON outputs.
13. Log failures with retry-safe job IDs.
14. Avoid hidden magic state.
15. Prefer deterministic workflow over agent-to-agent free conversation.

---

# 80. CODEX BUILD ORDER

## Sprint 0 — Foundation
- Next.js app
- TypeScript
- DB
- auth
- base layout
- project switcher
- environment config

## Sprint 1 — Project Brain
- brands
- projects
- audiences
- offers
- project detail
- project settings

## Sprint 2 — Design System
- design system CRUD
- Markdown editor
- versioning
- project override
- context resolver

## Sprint 3 — Research + Ideas
- research CRUD
- source URL
- claims
- idea CRUD
- convert research → idea

## Sprint 4 — Content Builder
- content CRUD
- hook
- script
- caption
- CTA
- funnel
- AI generation
- versioning
- run history

## Sprint 5 — Visual Studio
- visual plan
- visual item
- image provider interface
- generation
- asset library
- regeneration
- reference attachment

## Sprint 6 — Calendar
- calendar
- status
- filters
- drag/drop
- funnel colors

## Sprint 7 — Reuse Engine
- search existing assets
- similar content
- suggestions
- reuse / remix

## Sprint 8 — Approval + Export
- approval workflow
- production pack
- ZIP export

---

# 81. FIRST CODEX TASKS

Give Codex one task at a time.

## Task 1

```text
Create a Next.js + TypeScript application called Content Command Center.

Requirements:
- App Router
- Tailwind
- PostgreSQL
- project switcher
- left navigation
- dashboard shell
- light UI
- cream / white background
- black text
- orange accent
- rounded cards

Create placeholder routes:
/
projects
design
research
ideas
content
visual
calendar
library
system/runs

Do not implement AI yet.
Focus on app architecture and reusable UI components.
```

## Task 2

```text
Implement Project Brain.

Entities:
Brand
Project
Audience
Offer

Project must contain:
name
brand
goal
audience
offers
content pillars
default funnel
design system id

Create:
- DB schema
- CRUD
- project list
- project detail
- project switcher

Use typed validation.
```

## Task 3

```text
Implement Design System Memory.

Create:
DesignSystem
DesignSystemVersion
ProjectDesignOverride

Sections:
Brand Direction
Color System
Typography
Layout
Shapes
Cards
Image Style
Motion Style
Format Presets
Do / Don't

Allow Markdown editing.
Store versions.
Add a "Resolve Design" service that merges:
global
brand
project
campaign
current task
with correct priority.
```

## Task 4

```text
Implement Research + Idea Bank.

Research item:
topic
summary
source_url
claim
evidence
confidence
last_verified
status
tags

Idea:
title
description
research_ids
project_id
funnel
pillar
offer_id
priority
status

Add "Convert to Idea".
```

## Task 5

```text
Implement Content Builder.

Inputs:
project
idea
research
audience
platform
funnel
offer
format
goal

Outputs:
hook
script
caption
CTA
visual plan placeholder

Create:
ContentItem
ContentVersion
AgentRun

Every AI call must create AgentRun.
Use typed JSON output schema.
Keep AI provider behind an interface.
```

---

# 82. AI PROVIDER INTERFACES

## Text

```ts
export interface TextModelProvider {
  generateStructured<T>(args: {
    system: string
    prompt: string
    schema: unknown
    metadata?: Record<string, unknown>
  }): Promise<T>
}
```

## Image

```ts
export interface ImageModelProvider {
  generate(args: {
    prompt: string
    aspectRatio?: string
    references?: string[]
    metadata?: Record<string, unknown>
  }): Promise<{
    assetUrl: string
    provider: string
    model: string
    metadata?: Record<string, unknown>
  }>
}
```

## Embeddings

```ts
export interface EmbeddingProvider {
  embed(text: string): Promise<number[]>
}
```

---

# 83. STRUCTURED AI OUTPUTS

Avoid freeform AI output where the app depends on structure.

Example content generation schema:

```json
{
  "hook": "",
  "script_sections": [
    {
      "label": "Hook",
      "start_sec": 0,
      "end_sec": 3,
      "text": ""
    }
  ],
  "caption": "",
  "cta": "",
  "visual_plan_summary": "",
  "fact_check_items": []
}
```

---

# 84. AGENT RUN STATE MACHINE

```text
queued
running
waiting_for_approval
completed
failed
cancelled
```

Run should be retry-safe.

---

# 85. APPROVAL STATE MACHINE

```text
draft
submitted
approved
changes_requested
rejected
```

---

# 86. CONTENT STATUS

```text
idea
draft
scripted
visual_planning
producing
review
ready
scheduled
published
archived
```

---

# 87. VISUAL STATUS

```text
planned
generating
generated
qa_failed
approved
rejected
```

---

# 88. RESEARCH STATUS

```text
fresh
needs_verification
outdated
conflicting
unsupported
```

---

# 89. OBSERVABILITY

Log:
- agent run
- model
- prompt version
- duration
- retry count
- error type
- usage
- output object id

Never log secrets or API keys.

---

# 90. ERROR HANDLING

Examples:

## AI output invalid
- retry once with schema reminder
- if still invalid, mark failed
- preserve raw output internally

## Image generation failed
- do not lose visual plan
- retry selected item only

## Research source unavailable
- mark source unavailable
- do not delete claim automatically

## Project context missing
- block generation
- ask user to select project

---

# 91. FUTURE INTEGRATION INTERFACES

Prepare interfaces for:

```text
Browser Tool
Research Search
Google Drive
Notion
Slack
Gmail
Calendar
Publisher
Analytics
Video Renderer
Voice Provider
Transcription Provider
```

Do not implement all in MVP.

---

# 92. FUTURE AGENT EXECUTION MODEL

Preferred:

```text
Supervisor
↓
Deterministic workflow graph
↓
Specialist agent steps
↓
Typed result
↓
Human checkpoint
```

Avoid:

```text
10 agents freely chatting until they "feel done"
```

---

# 93. PRODUCT DIFFERENTIATORS

## 1. Production Memory
Remembers how work was produced, not just brand voice.

## 2. Research → Creation
Research becomes production assets directly.

## 3. Design Instructions as Executable Context
Design guidelines are machine-usable instructions.

## 4. Content Lineage
Trace from source → content → visual → performance.

## 5. Reuse First
Search existing work before generation.

## 6. Motion-aware Visual Production
Generate assets for animation, not static-only.

## 7. Agent Skills Architecture
Agents are configurable roles using reusable skills.

## 8. Performance-driven Next Action
Analytics determine what to create next.

---

# 94. SUCCESS METRICS

## User productivity
- time from idea to ready-to-publish
- % assets reused
- number of manual app switches reduced
- number of duplicate research tasks prevented

## Quality
- brand QA pass rate
- fact QA pass rate
- approval revision count

## Production
- content pieces per week
- visual generation success rate
- reuse rate
- average content cost

## Performance
- improvement in saves
- improvement in shares
- improvement in completion rate
- lead conversion from content

---

# 95. NORTH STAR

The ideal user experience:

> The user opens the system and does not need to decide where to start.

The system already knows:
- what is trending
- what the user has researched
- what content is missing
- what funnel stage is under-covered
- which offer should be supported
- which design system applies
- which assets already exist
- which agent should do the next task
- where human approval is needed

The user should be able to move from:

```text
"ทำคอนเทนต์เรื่องนี้"
```

to:

```text
Research ✓
Script ✓
Visual plan ✓
Images ✓
Brand QA ✓
Fact QA ✓
Production Pack ✓
Ready to Publish
```

without losing control, context, or brand consistency.

---

# 96. FINAL BUILD RECOMMENDATION

Build the product in this order:

```text
PROJECT BRAIN
→ DESIGN SYSTEM
→ RESEARCH
→ CONTENT BUILDER
→ VISUAL STUDIO
→ ASSET LIBRARY
→ CALENDAR
→ APPROVAL
→ REUSE ENGINE
→ PERFORMANCE
→ AGENTS
→ AUTOMATION
```

Do not start with a complex multi-agent framework.

First make the production data model, design context, project context, and content workflow correct.

Then add agent orchestration on top.

This keeps the product debuggable, replaceable, and scalable.
