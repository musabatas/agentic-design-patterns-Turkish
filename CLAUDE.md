# Agentic Design Patterns - Turkish Translation Project

## Project Overview

This is a Turkish translation of the "Agentic Design Patterns" book. The book covers 21 agentic AI design patterns across 40+ markdown files organized in 6 parts (Introduction, Parts 1-4, Appendix) plus back matter (Conclusion, Glossary, Index, FAQ).

## Translation Guidelines

### General Principles

- Translate into clear, natural Turkish that reads fluently — not word-by-word machine translation.
- Preserve the original meaning, tone, and technical accuracy at all times.
- The target audience is Turkish-speaking software engineers and AI practitioners. Write accordingly.
- Keep the same markdown structure, headings hierarchy, and formatting as the original.
- Do not translate code blocks, variable names, function names, or file paths.
- Do not translate image file names or asset references.
- Preserve all links, references, and cross-references as-is.

### Terminology Strategy

**Keep the following in English (do not translate):**
- Widely adopted technical terms that would lose meaning or clarity in Turkish:
  - prompt, token, embedding, fine-tuning, transformer, attention
  - agent, multi-agent, agentic
  - API, SDK, CLI, LLM, RAG, MCP, A2A, GUI
  - framework names: LangChain, LangGraph, CrewAI, Google ADK
  - model names: GPT, Gemini, Claude
  - chain-of-thought (CoT), tree-of-thoughts (ToT), ReAct
  - orchestrator, router, pipeline
  - context window, grounding, hallucination
  - tool use, function calling
  - guardrails, human-in-the-loop
  - vector database, knowledge base
  - workflow, checkpoint, rollback
  - retry, fallback, timeout
  - benchmark, metric, evaluation
- Brand names, product names, and proper nouns
- Code-related terms (class, function, method, decorator, async, etc.)

**Translate these terms to Turkish (with English in parentheses on first use in each chapter):**
- Design pattern → Tasarim kaliplari (Design Patterns)
- Memory management → Bellek yonetimi (Memory Management)
- Planning → Planlama (Planning)
- Reflection → Yansitma (Reflection)
- Parallelization → Paralelizasyon (Parallelization)
- Routing → Yonlendirme (Routing)
- Safety → Guvenlik (Safety)
- Goal → Hedef (Goal)
- Knowledge retrieval → Bilgi erisimi (Knowledge Retrieval)
- Exception handling → Hata yonetimi (Exception Handling)
- Recovery → Kurtarma (Recovery)
- Prioritization → Onceliklendirme (Prioritization)
- Exploration → Kesif (Exploration)
- Discovery → Kesfetme (Discovery)
- Learning → Ogrenme (Learning)
- Adaptation → Uyum saglama (Adaptation)
- Monitoring → Izleme (Monitoring)
- Resource → Kaynak (Resource)
- Optimization → Optimizasyon (Optimization)
- Reasoning → Akil yurutme (Reasoning)
- Collaboration → Is birligi (Collaboration)
- Communication → Iletisim (Communication)

> When in doubt, keep the English term. Forced translations that sound unnatural are worse than keeping the original.

### File Naming Convention

- **Do not modify original English files.** They remain untouched.
- Create a separate Turkish translation file for each original by appending `-tr` to the filename (before the extension).
- Place the translated file in the **same directory** as the original.

**Example:**
```
00-Introduction/05-Introduction.md          → original (English)
00-Introduction/05-Introduction-tr.md       → translation (Turkish)
```

### Formatting Rules

- Use Turkish quotation marks where appropriate: "..." or «...»
- Preserve bullet points, numbered lists, tables, and blockquotes.
- Preserve copyright notices and license text as-is (do not translate).
- Keep author names and acknowledgment names as-is.

### Translation Workflow

1. Translate one file at a time — create a new `-tr.md` file for each.
2. Work in order: Introduction (00) → Part One (01) → Part Two (02) → Part Three (03) → Part Four (04) → Appendix (05) → Root files (Conclusion, Glossary, Index, FAQ).
3. After translating each file, review for:
   - Consistent terminology usage
   - Natural sentence flow in Turkish
   - No broken markdown formatting
   - No accidentally translated code blocks or technical terms that should stay in English

### File Structure

```
00-Introduction/     → 6 files (Dedication through core definitions)
01-Part_One/         → 7 chapters (Foundational patterns: Ch 1-7)
02-Part_Two/         → 4 chapters (Advanced systems: Ch 8-11)
03-Part_Three/       → 3 chapters (Production concerns: Ch 12-14)
04-Part_Four/        → 7 chapters (Multi-agent architectures: Ch 15-21)
05-Appendix/         → 7 appendices (A through G)
Root files           → Conclusion, Glossary, Index of Terms, FAQ

Each directory will contain both original (.md) and translated (-tr.md) files side by side.
```

### Quality Checks

- Translated text should feel like it was originally written in Turkish.
- Technical explanations must remain precise — do not simplify or omit details.
- If a sentence structure doesn't work in Turkish, restructure it while keeping the meaning.
- Maintain consistent terminology across all chapters. If you translate a term one way in Chapter 1, use the same translation everywhere.
