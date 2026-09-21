# Thesis Writing Instructions

## Scope

These instructions apply to every text written for the master's thesis,
including chapters, sections, abstracts, captions, and short connecting
passages. The thesis is written in English.

Do not include repository setup, Bash commands, build instructions, or editor
configuration unless they are explicitly requested. When writing thesis text,
return material that can be copied directly into a LaTeX source file.

## Language and academic style

- Use clear, precise, and direct academic English.
- Maintain the register of a master's thesis without making the prose overly
  formal, ornate, or impersonal.
- Prefer simple sentence structures when they express the idea accurately.
- Vary sentence length to obtain a natural rhythm. Avoid a sequence of sentences
  with the same length or construction.
- Keep the tone calm and factual. Do not use promotional or unsupported language
  such as *groundbreaking*, *revolutionary*, or *remarkable*.
- Avoid common AI-writing formulas, generic introductions, empty transitions,
  and unnecessary summaries.
- Do not use corporate language or inflated expressions when a technical term or
  a direct verb is sufficient.
- Do not repeat the same claim in slightly different words.
- Explain why a technical element is relevant instead of only listing its
  properties.
- Distinguish clearly between established facts, statements supported by the
  literature, design choices made in this work, and conclusions drawn from the
  experiments.
- Do not claim that a method improves performance unless the cited work or the
  thesis results support the claim.
- Preserve continuity with the preceding text. A section should not restart the
  discussion with a broad definition when the concept has already been
  introduced.
- Introduce acronyms at their first occurrence, for example `Model Predictive
  Control (MPC)`, and use only the acronym afterwards when no ambiguity remains.
- Use terminology consistently. In particular, write `wheeled-legged robot`,
  `legged locomotion`, `Model Predictive Control`, `Reinforcement Learning`,
  `Whole-Body Controller`, and `Single Rigid Body Dynamics` consistently with
  their established acronyms.
- Use `controller` for the complete control method and `policy` for the learned
  RL component. Do not use the two words as synonyms.
- Write code identifiers, variables, and mathematical quantities only when they
  help the scientific explanation. Do not turn implementation details into a
  list unless the section specifically documents the implementation.

## Human-like writing

The prose must read as if it had been written and revised by a human researcher,
not assembled from recurring templates. This is a core requirement, not an
optional stylistic preference.

- Vary syntax as well as sentence length. Do not repeatedly use the same
  subject--verb structure or begin consecutive sentences in the same way.
- Avoid predictable transitions such as `Moreover`, `Furthermore`,
  `Additionally`, and `In conclusion` when the logical relation is already
  clear. Use them only when they add precision.
- Do not open sections with generic formulas such as `In recent years`,
  `It is important to note`, or `This section aims to`. Begin with the actual
  technical point.
- Avoid symmetrical, mechanically balanced lists when the ideas do not naturally
  have the same weight.
- Do not force every paragraph into the pattern of topic sentence, three generic
  supporting sentences, and a concluding sentence.
- Prefer concrete subjects and verbs. For example, write `MPC computes` rather
  than `the computation is carried out by the MPC framework`.
- Allow short sentences when they improve emphasis or close an argument. Do not
  lengthen a sentence merely to make it sound more academic.
- Use cautious language only where uncertainty exists. Avoid repeatedly using
  `may`, `might`, `can potentially`, or `could possibly` as generic hedging.
- Do not overuse paired constructions such as `not only ... but also`,
  `both ... and`, or `while X ..., Y ...`.
- Avoid restating the paragraph's content in its final sentence unless the final
  sentence establishes a consequence or a transition.
- Keep transitions specific to the argument. The relation between two sentences
  should follow from their content rather than from a generic connective.
- After drafting, read the passage as continuous prose and revise any repeated
  cadence, stock phrase, artificial contrast, or abrupt change of register.
- Human-like writing does not mean informal writing. Preserve technical accuracy,
  academic restraint, and consistent terminology throughout.

## LaTeX source width

Hard-wrap the source at approximately 80--90 characters so that it remains
readable in the VS Code editor. A source line should normally not exceed 90
characters.

The line break must be inserted only between words. It must not:

- split a word;
- add or remove text;
- create a new paragraph;
- interrupt a LaTeX command and its argument when this would reduce clarity;
- separate a citation from the statement that it supports.

A single newline in the LaTeX source is treated as a space and therefore does
not change the rendered paragraph. Line wrapping is only a source-formatting
choice.

Example:

```latex
Model Predictive Control predicts the evolution of the system over a finite
horizon and computes the control inputs while accounting for the model and its
constraints.
```

## Paragraph separators and backslashes

When the text must start a new paragraph, use the following project convention:

```latex
distribution, friction limits, and actuator bounds.\\
\
The explicit formulation of these constraints allows the controller to account
for the physical limits of the system.
```

Therefore:

1. end the previous paragraph with `\\`;
2. place a single `\` on the following source line;
3. start the new paragraph on the next line;
4. do not also insert an empty source line around this separator.

Use this separator only for a real paragraph transition, not every time the
source reaches the 80--90 character limit. Ordinary source wrapping requires
only a newline and no backslash.

Do not alternate this convention with blank-line paragraph separators within
the same generated text. When editing existing text, preserve the local style
unless the user asks to normalise it.

## Structure and exposition

- Begin a chapter with a short unnumbered introductory passage before its first
  section when the chapter needs orientation. It should state the purpose and
  progression of the chapter rather than repeat the thesis abstract.
- Each section should develop one identifiable topic and lead naturally to the
  next one.
- Move from the general concept to the specific methods relevant to the thesis.
- In related work, organise papers by technical role or methodological relation,
  not as disconnected paper-by-paper summaries.
- Compare methods using the same criteria: model, control hierarchy, learned
  component, output, training arrangement, constraints, and validation setting.
- Keep background chapters independent of the exact implementation where
  possible. Reserve project-specific architecture and parameter details for the
  methodology or architecture chapters.
- Avoid excessive headings, bullet lists, and itemisations in the thesis body.
  Prefer connected prose unless an exact enumeration is scientifically useful.
- Do not add a conclusion paragraph to every short section. Conclude only when
  it clarifies the connection to the thesis or the following section.

## Citations

### General rules

- Cite the primary source for a method, numerical result, architecture, or claim.
- Use review papers only for broad historical or field-level statements when a
  primary source is not more appropriate.
- Place the citation immediately after the claim it supports, before the final
  punctuation according to the existing thesis convention, for example
  `... in parallel on the GPU \cite{mpx}.`
- Do not place an isolated citation at the end of a long paragraph when it is
  unclear which sentences it supports.
- A citation does not compensate for an unsupported interpretation. State only
  what the cited paper actually establishes.
- Do not cite one paper for claims that belong to a different source.
- When several references support the same statement, group them in one command,
  for example `\cite{key_one,key_two}`.
- Do not add citations to descriptions of this thesis's own implementation unless
  the sentence also refers to a method, model, or result taken from the
  literature.
- Verify authors, complete title, publication venue, year, volume, pages, and DOI
  or arXiv identifier against the paper or an authoritative publisher record.
- Distinguish the arXiv posting year from the formal publication year. Use the
  formal publication data when available.
- Keep citation keys short, descriptive, and easy to recall. Do not build them
  mechanically from the authors, publication year, and title.
- Prefer a single meaningful name, such as `mpx` or `residual_mpc`, over a long
  identifier such as `amatucci2026mpx`.
- A citation key is an internal project identifier. It does not need to contain
  the author or publication year, and bibliographic corrections must not cause
  it to change.
- Never invent a missing bibliographic field. Leave it absent or flag it for
  verification.

### Citation-key remapping

When creating or rewriting the `.bib` file, replace complicated citation keys
with short names that recall the paper or its role in the thesis. Use the
following project mapping:

- `amatucci2026mpx` becomes `mpx`.
- `eisman2026racing` becomes `racing`.
- `kamohara2025rlaugmented` becomes `adaptive_mpc`.
- `jeon2025residual` becomes `residual_mpc`.
- `patrizi2026rlaugmented` becomes `non_gaited`.

These short names must be used both in the `.bib` entries and in every
corresponding `\cite{...}` command. For example, write `\cite{mpx}`, not
`\cite{amatucci2026mpx}`.

If an older `.bib` file contains one of the long keys, remap it to the
corresponding short key above and update every `\cite{...}` that refers to it.
Do not create duplicate entries for the same publication.

For a new source not included above, choose a short semantic key derived from
the method, system, or distinctive topic of the paper. Avoid author names and
years unless they are necessary to distinguish two otherwise identical keys.
Once a key has been selected, keep it stable throughout the thesis.

## Use of the project references

The supplied papers are the main sources for general statements on MPC,
GPU-parallelised optimal control, residual learning, and hybrid legged
locomotion. Read the relevant paper before attributing a specific architecture,
metric, limitation, or experimental result to it.

The files `residual_learning_overview_tita.md` and
`residual_learning_overview_lite3.md` describe the thesis implementations. Use
them to explain the control architecture, information flow, policy inputs and
outputs, torque generation, and the relation between MPC, WBC, and RL. Treat
them as project documentation, not as external scientific evidence.

Do not transfer details from TITA to Lite3 or vice versa. State explicitly which
platform is being discussed whenever the architectures differ.

## Final checks before returning thesis text

Before returning a passage, verify that:

- it is written in academic English;
- every source line is approximately 80--90 characters or shorter;
- ordinary line wrapping uses no backslashes;
- every real paragraph break uses the `\\` followed by `\` convention;
- terminology and acronyms are consistent;
- the prose has varied syntax and rhythm and contains no recurring AI-style
  formulas or mechanical paragraph patterns;
- citations are adjacent to the claims they support;
- citation keys follow the stable remapping;
- factual claims match the cited sources;
- TITA and Lite3 architectures have not been mixed;
- no setup, Bash, or repository-management material has been added;
- the result can be copied directly into the LaTeX source.