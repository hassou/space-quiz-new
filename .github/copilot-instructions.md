# Copilot instructions

## Run and verify

- Open `index.html` directly in a browser; the app has no build step or runtime dependencies.
- No automated test, lint, or build commands are configured. For a browser smoke check, start a quiz, try both a correct and incorrect answer, finish all questions, and use **Play again**.

## Architecture

- `index.html` is the complete application: semantic markup, inline CSS, question data, and quiz logic all live in one file.
- The welcome, quiz, and results views are separate elements switched with the `hidden` attribute. Quiz state (`questionIndex`, `score`, and `answered`) is managed in the inline script.
- `questions` is the source of truth for prompts, choices, zero-based correct-answer indexes, categories, and feedback facts. `renderQuestion()` creates each question's answer buttons; `selectAnswer()` handles scoring and feedback; `showResults()` selects the final reaction by score.
- CSS custom properties define the shared palette in `:root` and its dark-mode overrides in `prefers-color-scheme`. Motion effects must continue to respect `prefers-reduced-motion`.

## Code conventions

- Keep question content in the `questions` array and keep each `answer` value aligned with its choice's zero-based index.
- Use native buttons for quiz actions and answers. The progress indicator uses `role="progressbar"` and updated `aria-valuenow`; answer feedback is announced through the status region.
- Preserve focus handoffs when changing views or questions: starting and advancing focus the first answer, and finishing focuses **Play again**.
- Keep presentation tokens in the existing CSS custom properties, with corresponding light and dark values for new theme colors.
