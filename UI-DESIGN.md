# Restoration Game UI design notes

This is a design and interaction reference for the Team L frontend. It is not the final iOS application or a validated educational assessment.

## Requirements and assumptions

The [published specifications](https://tarheels.live/teamlcom523/specifications/) describe the following requirements:

| Requirement | Prototype representation |
| --- | --- |
| Identify judge and bailiff by tapping, with retry feedback | Courtroom hit areas and feedback dialogs |
| Four-choice hearing and attorney-role questions | Single-choice question pattern |
| Select-all defendant-rights question | Multiple selection and explicit submission |
| Eyewitness, video, weapon, and overall evidence strength | Four evidence tasks |
| Five plea types with five-choice consequence questions | Not guilty, guilty, no contest, Alford, and NGRI lessons |
| Plea-offer fairness and three outcome branches | Offer, plea decision, and three outcome templates |
| Simple language, large text, comfortable tap targets, non-color feedback | Large rows, short instructions, text and selection indicators |
| Offline iPad use and saved progress | Self-contained HTML and local demonstration storage |
| Staff-only results | Demo PIN screen and attempt table |

Colors, typography, dimensions, stage grouping, exact PIN behavior, and the demo score formula are design assumptions. Confirm the hospital's iPad models, iPadOS support, orientation policy, and approved content before implementation.

Clinician results appear in the published platform and architecture decisions but are marked optional in part of the requirements. The team should reconcile that MVP priority. The published interface list also mentions patient scores while the platform decision restricts results to staff; this prototype uses a score-free patient completion screen.

## Screen flow

Home → opening story → judge → bailiff → charges and bond → hearing question → rights question → attorney meeting → attorney role → evidence → five plea lessons → plea offer → plea decision → outcome → completion.

The final decision branches into Not Guilty, Guilty/No Contest/Alford, or NGRI. It is a branching choice rather than a factual question with one correct plea.

The reviewer screen selector above the app is for team review and is outside the proposed patient interface.

## Interaction patterns

1. A single-choice tap selects a row. Check answer submits it. An incorrect answer shows feedback and allows another attempt on the same task.
2. A select-all question evaluates the complete submitted set, including extra selections. Changing a selection does not count as another attempt.
3. A courtroom character tap is a submitted attempt.
4. All five plea questions must be completed before the offer becomes available. Reading a card alone does not complete the lesson.
5. The prototype uses explicit confirmation for the final plea decision and for replacing a saved practice session.
6. Staff access is a demo only. Production access, PIN setup, locking, and persistence require the team's backend.

## Layout and accessibility targets

The Figma working size is 1024 × 768 landscape, with an 820 × 1180 portrait example. These dimensions are design references, not a confirmed device inventory.

- Keep one main task on a screen.
- Use answer rows at least 72 units high, with room for wrapped text.
- Use text and a check mark to indicate selection; avoid relying on color alone.
- Keep the main action in a consistent location.
- Let long content scroll without hiding the action.
- Preserve safe areas, Dynamic Type, VoiceOver order, and Switch Control in SwiftUI.
- Use descriptive character accessibility labels that do not reveal the tested courtroom role.

### Color tokens

| Role | Value |
| --- | --- |
| Background | #F7F4EB |
| Surface | #FFFFFF |
| Main text and primary action | #19263C |
| Supporting text | #4A5563 |
| Teal accent | #28666E |
| Start action | #F2C14E |
| Border | #657382 |

Measured contrast pairs in the HTML prototype: main text/background 13.80:1; supporting text/background 6.89:1; white/primary button 15.18:1; selected teal label/selected background 5.72:1; border/white 4.85:1. These measurements do not replace testing the complete native app.

The Figma draft uses Source Sans 3; the HTML prototype uses a system sans serif font. The font choice remains open to team review.

## Backend integration

The UI needs question ID, topic, prompt, answer mode, choice IDs and labels, approved feedback, media assets, and completion state. Submit selected IDs to game logic and render its response. Keep scoring and persistence in one shared service.

The demo first-try score divides checks completed correctly on their first submitted attempt by completed checks. The denominator for unfinished sessions, the set of scored checks, and any pass threshold need an agreed policy. The final plea choice is not scored as right or wrong.

## Figma draft limitations

The [Figma draft](https://www.figma.com/design/LqpNZ8xzXNIztqXSIhGzqN) has 41 screens, four feedback overlays, six shared component families, and three starting points. Its layers are editable text, vectors, and component instances.

Further edits were stopped by Figma's Starter tool-call limit. Remaining items:

- The home hero headline overlaps its paragraph. Give the two-line headline a 128-unit text box, put the paragraph below with a 24-unit gap, and let the welcome column grow to its content.
- Update the border token to #657382 to match the HTML prototype.
- Hearing options C and D currently use the sample wrong-B state.
- Evidence Check answer can advance without selection in the Figma draft.
- Rights and plea quizzes use fixed sample states; the PIN keypad is illustrative.
- Some resized text and cards need a final visual check.

Use the HTML prototype as the reference for functioning selections, retries, completion gates, and branching. The Figma draft should not be presented as a finished patient application.

## Content that still needs approval

Replace the workbook answer placeholders, evidence facts and ratings, plea definitions, legal consequences, offer terms, outcome dialogue, and sample answer keys with client-approved content. No client source documents or private communications are included in this repository.
