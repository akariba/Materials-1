Design and implement a new capability inside the Lending Correlation application called:

# AI Create Relationship

The purpose of this capability is to allow a lending user to define new entity relationships in natural language, have AI convert that intent into a structured and governed relationship configuration, preview the impact of the configuration, and then publish the approved definition so that it can generate relationship instances that appear in the Lending Correlation relationship map.

This capability must feel like a native extension of the existing Lending Correlation experience. It must not feel like a generic chatbot or a separate AI application.

The experience should be enterprise-grade, explainable, controlled, auditable, and suitable for financial-services users.

---

# 1. FEATURE LOCATION

Add an action called:

**AI Create Relationship**

Place this action within the existing Relationship Configuration / Relationship Definition area.

Do not immediately navigate the user to another page.

When the user clicks **AI Create Relationship**, expand an intelligent configuration workspace within the current experience.

The expansion can appear as:

* a large inline expandable panel;
* a right-side configuration workspace;
* or a modal-sized configuration canvas if required by the existing design system.

Prefer an inline or side-panel experience because the user should retain context of the existing Relationship Configuration library.

The user should be able to close or collapse the AI panel and return to the normal Relationship Configuration view without losing the rest of the page state.

---

# 2. PRIMARY USER OBJECTIVE

The user should be able to describe a desired relationship in normal business language.

Example:

“Identify companies that belong to the same economic group based on ownership, subsidiaries, common management, guarantees, addresses, SEC disclosures, and other reliable evidence.”

Another example:

“Create a relationship between borrowers that share the same guarantor, but only when the guarantor is currently active and the exposure exceeds $1 million.”

Another example:

“Identify companies under common control even when direct ownership is below 50%, using ownership, management overlap, parent-company disclosures, and guarantee relationships.”

The AI must convert this natural-language intent into a structured relationship definition.

The AI must not simply save the user's sentence as a prompt.

The AI should act as a configuration assistant that translates business intent into governed configuration.

---

# 3. CORE EXPERIENCE

Structure the AI Create Relationship experience into four logical stages:

1. Describe
2. Configure
3. Preview
4. Publish

Represent these stages visually as either:

* tabs;
* a horizontal stepper;
* or clear progressive sections inside one workspace.

The user should understand exactly where they are in the creation process.

---

# 4. STAGE 1 — DESCRIBE

Create a prominent natural-language input area.

Label:

**Describe the relationship you want to identify**

Helper text:

“Describe the entities, connection, evidence, thresholds, exclusions, or conditions that should define this relationship.”

Use a large multiline text area.

Provide intelligent placeholder text such as:

“Example: Identify companies under common ownership when one company owns at least 25% of another, or when reliable disclosures indicate common control.”

Below the text field provide optional suggested prompts or quick-start examples.

Suggested examples:

* Common Ownership
* Common Guarantor
* Shared Management
* Economic Group
* Parent / Subsidiary
* Cross Guarantee
* Common Collateral
* Supplier / Customer
* Joint Venture
* Shared Address
* Shared Directors

Selecting a suggestion should populate or initiate an example description, but the user must remain able to edit it.

Primary action:

**Generate Configuration**

Secondary action:

**Start from Existing Relationship**

If the user selects “Start from Existing Relationship,” allow selection of an existing relationship configuration and ask the AI to modify or extend it rather than starting from scratch.

Example instruction:

“Start from Common Ownership but change the ownership threshold from 25% to 50% and include management control as an alternative condition.”

---

# 5. AI INTERPRETATION STATE

After the user selects Generate Configuration, show a short AI-processing state.

Do not use playful or consumer-oriented AI language.

Use enterprise language such as:

“Analyzing relationship intent…”

Then:

“Structuring entities, evidence, conditions, and governance settings…”

Then render the generated configuration.

If useful, provide a concise interpretation summary above the configuration.

Example:

**AI Interpretation**

“This configuration identifies corporate relationships based on direct ownership, declared subsidiary relationships, or evidence of common control. Relationships must meet an 85% confidence threshold and require at least two supporting evidence signals unless ownership exceeds 50%.”

This interpretation summary should remain editable indirectly through the configuration, not as the primary saved logic.

---

# 6. STAGE 2 — CONFIGURE

The Configure view is the most important part of the feature.

The AI-generated result must be broken into structured configuration sections.

Use enterprise form components, cards, editable fields, dropdowns, chips, toggles, condition builders, and rule groups.

Do not show the relationship primarily as free-form JSON.

A technical or machine-readable view may optionally be available under an Advanced section.

Organize the configuration into the following sections.

---

# 7. BASIC RELATIONSHIP DEFINITION

Section title:

**Relationship Definition**

Fields:

### Relationship Name

Example:
Common Ownership

Editable text field.

### Relationship Code

Example:
COMMON_OWNERSHIP

Automatically generated but editable for authorized users.

### Description

Concise description of what this relationship represents.

Example:
“Represents two corporate entities connected through material direct or indirect ownership.”

### Relationship Category

Dropdown.

Possible values:

* Corporate
* Ownership
* Credit
* Guarantee
* Collateral
* Management
* Operational
* Commercial
* Legal
* Financial
* Supply Chain
* Other

Allow multiple categories if the architecture supports it, but one primary category should always exist.

### Relationship Type

Examples:

* Parent / Subsidiary
* Common Ownership
* Common Control
* Affiliate
* Common Guarantor
* Cross Guarantee
* Common Collateral
* Shared Management
* Shared Address
* Supplier
* Customer
* Joint Venture
* Custom

### Relationship Direction

Options:

* Directional
* Bidirectional
* Symmetric

If directional, expose:

Source → Target

Example:

Parent → Subsidiary

### Relationship Strength

Optional configuration:

* Binary relationship
* Weighted relationship
* Percentage-based relationship
* Confidence-based relationship
* Custom scoring

Example:

Ownership relationship could display 72%.

Shared Management relationship could display 92% confidence.

---

# 8. ENTITY CONFIGURATION

Section:

**Entities**

Create a Source Entity and Target Entity configuration.

Fields for each:

### Entity Type

Examples:

* Borrower
* Company
* Legal Entity
* Guarantor
* Individual
* Sponsor
* Fund
* Facility
* Loan
* Collateral
* Property
* Account
* Counterparty
* Supplier
* Customer

Allow entity taxonomy to come from the existing Lending Relationship Intelligence data model.

Example:

Source Entity:
Company

Target Entity:
Company

Provide the option:

**Allow same entity type**

Example:
Company → Company

Another relationship might be:

Borrower → Guarantor

or:

Loan → Collateral

---

# 9. RELATIONSHIP RULE BUILDER

Create a major section called:

**Relationship Logic**

This should visually function as a structured rule builder.

The AI should generate conditions from the user's natural-language description.

Example:

Relationship is created when:

ANY OF THE FOLLOWING ARE TRUE:

1.

Direct Ownership Percentage
is greater than or equal to
25%

OR

2.

Explicit Subsidiary Disclosure
equals
True

OR

3.

Common Parent Confidence
is greater than or equal to
90%

AND

Evidence Quality
is greater than or equal to
High

The user must be able to:

* add conditions;
* remove conditions;
* reorder conditions;
* change operators;
* create nested AND / OR groups;
* edit thresholds;
* select attributes;
* choose source fields;
* create exclusions.

Support rule structures such as:

ALL
ANY
NONE

Example:

ALL OF:

* Same guarantor
* Guarantor status = Active
* Total relationship exposure > $1M

The visual rule builder should make complex logic readable.

---

# 10. AI-CONSTRUCTED ADVANCED LOGIC

The system should support AI-derived conditions that are not simple database equality checks.

Examples:

* management overlap;
* name similarity;
* address similarity;
* ownership inference;
* beneficial ownership;
* common control;
* parent-company disclosure;
* guarantee-network proximity;
* shared collateral;
* shared legal representatives;
* shared executives;
* supply-chain relationships;
* public disclosure evidence.

For AI-derived conditions, visually distinguish them from deterministic rules.

Example badge:

**AI Inference**

versus:

**Deterministic Rule**

Provide a tooltip:

“AI Inference uses evidence-based analysis rather than an exact source-system field match.”

---

# 11. EVIDENCE CONFIGURATION

Section:

**Evidence Requirements**

The user should be able to define what evidence is necessary before a relationship can be accepted.

Fields:

### Minimum Evidence Signals

Example:
2

### Evidence Combination

Options:

* Any qualifying evidence
* Multiple independent sources
* Primary source required
* AI confidence only
* Custom evidence rule

### Evidence Types

Selectable chips:

* Ownership records
* Regulatory filings
* Loan documentation
* Guarantee documentation
* Internal client records
* Public company filings
* Company websites
* Corporate registries
* Address records
* Management records
* News sources
* External data providers

### Evidence Independence

Toggle:

**Require independent evidence sources**

Example:

A company website and a regulatory filing count as two independent sources.

Two pages from the same company website should not necessarily count as two independent sources.

---

# 12. DATA SOURCE CONFIGURATION

Section:

**Data Sources**

Show a source hierarchy.

### Internal Sources

Examples:

* Borrower Master
* Customer Master
* Loan Systems
* Credit Systems
* CRM
* KYC
* Legal Documentation
* Guarantee Records
* Collateral Systems
* Existing Relationship Graph

### External Sources

Examples:

* Regulatory filings
* SEC filings
* Corporate registries
* Public corporate websites
* Trusted news
* Third-party data providers

Provide toggles for each source.

Allow classification of data sources as:

* Primary
* Secondary
* Supporting
* Excluded

Example:

SEC filings — Primary

Internal borrower records — Primary

Company website — Supporting

Unverified web content — Excluded

---

# 13. SOURCE TRUST CONFIGURATION

Allow the relationship definition to specify minimum source quality.

Example:

Minimum Source Quality:
High

Possible values:

* Verified
* High
* Medium
* Low
* Excluded

Allow the enterprise to centrally govern which sources belong to each level.

The relationship configuration should reference those governed classifications rather than hard-code websites individually where possible.

---

# 14. CONFIDENCE MODEL

Section:

**Confidence & Acceptance**

Provide:

### Minimum Confidence

Slider or numeric field.

Example:
85%
