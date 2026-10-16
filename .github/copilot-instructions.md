# Copilot instructions

## Project structure and architecture

This repository is a self-contained static web app: `index.html` contains the page markup, all CSS, the quiz data, and the application JavaScript. There is no framework, package manager, build step, or external runtime dependency. Open `index.html` directly in a browser to run it.

The quiz is driven by the `questions` array in the inline script. Each entry has a `category`, `text`, four `options`, a zero-based `answer` index, and a `fact` shown after selection. `showQuestion` renders the current entry; `selectAnswer` locks the choices, updates the score/progress, and displays feedback; `showResults` renders the final summary; the restart handler resets quiz state.

## Commands and verification

- Run: `Start-Process .\index.html` from PowerShell, or open `index.html` in a browser.
- There are no automated build, test, or lint commands or a test runner. For a focused manual check, reload the page, answer one question, and verify the correct/incorrect feedback and disabled answer buttons. For a full-flow check, continue through the results screen and use **Explore again** to confirm the quiz resets.

## Code conventions and change guidance

- Keep the app dependency-free and self-contained in `index.html`; preserve the inline HTML/CSS/JavaScript structure unless the project gains an explicit build system.
- Treat the `questions` array as the source of truth for quiz content. Keep each answer index within its own `options` array and update UI totals/percentage calculations if changing the number of questions; the current markup and accuracy calculation assume 10.
- The page uses `getElementById` through the `$` helper and direct DOM updates. Dynamic question and feedback text is assigned with `textContent`; preserve that pattern for content strings.
- Quiz state (`current`, `score`, `answered`, and `history`) is in-memory and reset by the restart handler. Keep progress, score, feedback, and result-summary updates consistent when changing quiz flow.
- Maintain the existing accessibility behavior: semantic buttons, the question/answer group relationship, live feedback, progress-bar values, descriptive answer/result labels, and focus movement after answering or changing screens.
- Styling is defined in the document's `<style>` block with CSS custom properties, dark-mode and reduced-motion media queries, and a narrow-screen breakpoint. Keep responsive and color-scheme behavior intact when changing styles.
