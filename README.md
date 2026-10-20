# Foundations-of-Artificial-Intelligence
Foundations of Artificial Intelligence Project CS23533
**MEDIXAI: Transparent Rule-Based Expert System**

> **Classical Knowledge-Based Reasoning for Medical Diagnosis Demonstration**
> 
> *Developed for Foundations of Artificial Intelligence (FOAI) · Unit IV: Knowledge-based reasoning*
> 

---

**Project Overview**

MEDIXAI is a zero-dependency, browser-based classical expert system that demonstrates forward and backward rule-based reasoning, premise verification, and contradiction checks. The system operates transparently by construction, relying on no machine learning models, no training data, no external libraries, and no server backend.

Every evaluation exposes its full deductive path:

* Identifies which symptom premises are fully satisfied.


* Highlights missing, unverified, or explicitly absent preconditions.


* Computes heuristic match scores directly from explicit rule weights.


* Halts evaluation upon identifying mutually exclusive clinical input conflicts.



---

**Key Features**

* **Comprehensive Knowledge Base:** Contains 38 disease rules covering 104 distinct symptom facts organized across 8 categories.


* **Forward Chaining Engine:** Evaluates all disease rules in a single pass to produce ranked candidates with heuristic match scores.


* **Interactive Backward Verification:** Prompts users to confirm or deny unknown required premises, automatically updating scores or blocking rules.


* **Input Consistency Checking:** Intercepts logical contradiction pairs before evaluation proceeds.


* **Safety Guardrails:** Flags high-urgency symptoms immediately, presenting emergency notices independent of heuristic candidate ranking.


* **Zero Runtime Dependencies:** Built purely with semantic HTML5, CSS3, and vanilla JavaScript that runs entirely in the local browser tab without saving or transmitting data.



---

**Inference Architecture & Mathematics**

**1. Rule Representation**

Each entry in the knowledge base defines an association between symptoms, required conditions, and clinical categories:

* **Weighted Symptoms:** Each symptom carries an assigned heuristic weight ranging from 4 to 10.


* **Required Premises:** Essential conditions that must all be present for a rule implication to fire.


* **Severity & Emergency Flags:** Indicators marking conditions requiring urgent medical review.



**2. Forward Evaluation Formula**

Candidate conditions are ranked based on the proportion of matched symptom weight relative to the disease rule's total weight:

$$\text{score} = 100 \times \frac{\sum w_{\text{matched}}}{\sum w_{\text{total}}}$$

If any required premise is missing from the working fact set, a dampening penalty multiplier is applied:

$$\text{score} = \text{score} \times 0.60$$

**3. Backward Premise Resolution**

When examining a candidate disease, any unestablished required premise can be inspected and updated:

* **Yes:** The symptom is added to the active fact set, removing the penalty multiplier and recalculating rankings.


* **No:** The symptom is marked as absent, which completely blocks the rule from firing.


* **Unsure:** The fact remains unknown, maintaining the missing-premise penalty without completely blocking the candidate.



**4. Contradiction & Consistency Checks**

Evaluation is prevented if conflicting pairs are selected simultaneously:

* Fever and No Fever


* High Fever and No Fever


* Diarrhea and Constipation



---

**Knowledge Base Scope**

The embedded rule base categorizes 38 conditions across 8 distinct categories:

| Category | Included Conditions |
| --- | --- |
| **Respiratory** | Common Cold, Influenza, COVID-19, Pneumonia, Asthma, Acute Bronchitis, Sinusitis, Allergic Rhinitis

 |
| **Viral** | Dengue Fever, Chickenpox, Measles, Mumps, Hand Foot and Mouth Disease, Viral Fever

 |
| **Bacterial** | Typhoid Fever, Tuberculosis, Cholera, Whooping Cough, Bacterial Meningitis

 |
| **Digestive** | Food Poisoning, Gastritis, Gastroenteritis, GERD, Peptic Ulcer

 |
| **Skin** | Eczema, Ringworm, Scabies, Psoriasis

 |
| **Neurological** | Migraine, Tension Headache, Vertigo

 |
| **Urinary** | Urinary Tract Infection, Kidney Stones, Cystitis

 |
| **Miscellaneous** | Heat Stroke, Dehydration, Iron Deficiency Anemia, Heat Exhaustion

 |

---

**Quick Start Guide**

Because the project is entirely self-contained inside a single file, setup requires no installation or build commands.

**Option 1: Direct Browser Launch**

Open `medixai.html` directly in any modern desktop or mobile web browser.

**Option 2: Local HTTP Server**

Run a local static server using Python:

```bash
python3 -m http.server 8000

```

Or using Node:

```bash
npx serve .

```

Navigate to `http://localhost:8000` to interact with the workspace.

---

**Repository Layout**

```text
medixai/
├── medixai.html       (Complete single-page application: UI, styling, and inference engine)
└── README.md          (Project documentation and system architecture)

```

---

**Academic Disclaimer**

> **Learning Tool Notice:**
> This software is an educational prototype created for Foundations of Artificial Intelligence coursework. The knowledge base consists of unvalidated toy rules and heuristic match scores, not clinical probabilities or diagnoses. It does not recommend medical treatments or replace professional clinical triage. In any medical emergency, contact local emergency services immediately.
> 
> 

---

**License**

Distributed under the MIT License. See `LICENSE` for details.
