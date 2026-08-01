# Lecture-to-Notes Prompt Toolkit

A small collection of reusable prompts I built for turning raw lecture
transcripts, practice assignments (PA), graded assignments (GA), and
previous-year questions (PYQs) into structured study material—without
having to re-explain the same formatting instructions to an AI assistant
every single time.

## Why I built this

Partway through my BS Degree coursework, I found that using an LLM to
generate notes from lecture transcripts made studying much easier. It
helped me follow lectures more actively and filled in gaps where the
instructor assumed prior knowledge.

During exams, I also started converting previous-year question papers
into structured study guides. This helped me identify recurring concepts,
understand why certain questions were important, recognize examiner
patterns, and practice more strategically instead of simply memorizing
solutions.

Over time, I found myself repeatedly pasting lecture transcripts into an
AI assistant and retyping the same instructions every session: explain
the intuition first, then the technical details, walk through the code
line by line, highlight common mistakes, and finish with practice
questions. Eventually, I turned those repeated instructions into reusable
prompt templates that I could paste once and use across different
courses.

Nobody assigned this project—it simply saved me from repeating the same
setup every time I studied.

## What's inside

| File | Purpose |
|------|---------|
| `prompts/lecture-to-notes.md` | Converts a raw lecture transcript into a structured study guide (intuition → concept explanation → code walkthrough → common mistakes → practice questions). |
| `prompts/coding-question.md` | A prompt for programming assignments that focuses on understanding the algorithm first, followed by implementation and a line-by-line explanation. |
| `prompts/quiz-prep-pyq.md` | A prompt for analyzing previous-year questions, grouping similar concepts, explaining every option, identifying recurring patterns, and building a comprehensive revision guide. |
| `examples/mad2-vuejs-example.md` | An example showing a real lecture transcript processed using `lecture-to-notes.md`, along with the generated output. |

## How I use this

I keep these prompts saved as templates and paste the relevant one at
the beginning of a new chat before providing a lecture transcript,
assignment, or set of previous-year questions. This saves several
minutes of repeatedly explaining my preferred output format and keeps
the generated study material consistent across different subjects.

## Notes

These prompts were developed and refined throughout my coursework,
starting around July 2026, well before this repository was made public.
This repository is simply the cleaned-up, shareable version of the
templates I had already been using in my personal study workflow.
