# Repository Guidelines: space-quiz

## Architecture & Structure
- **Zero-Dependency Single-File App**: All HTML, CSS, and JavaScript reside entirely within `index.html`. No package manager, bundler, server runtime, or external libraries are required.
- **Delivery Mechanism**: Directly viewable via `file://` protocol or any static file server in modern web browsers and the integrated browser canvas.

## Key Conventions & Constraints
- **Self-Contained Styling**:
  - Semantic CSS custom properties define theming under `:root` with automatic light and dark mode support via `@media (prefers-color-scheme: light)`.
  - Layout is constrained to a centered narrow column (`max-width: 480px`) with 14–16px sans-serif body typography.
  - Animations are implemented with vanilla CSS keyframes (`popSuccess`, `shakeWrong`, `floatEmoji`, `blinkSignal`).
- **Data & State Management**:
  - Questions are stored in the inline `questions` array of objects (`category`, `question`, `options`, `correctIndex`, `fact`).
  - Active quiz flow is governed by state variables: `currentQuestionIdx`, `score`, `answered`, and `advanceTimer`.
  - DOM updates are performed via standard Vanilla JS APIs without innerHTML parsing of user-supplied inputs.
- **Keyboard Navigation**:
  - `A`–`D` and `1`–`4` choose options during an active question.
  - `Enter`, `Space`, or `ArrowRight` advances to the next question when answered.
  - `Enter`, `Space`, or `R` restarts the quiz from the results screen.
- **Accessibility**:
  - Progress updates, scores, and feedback regions use appropriate ARIA attributes (`aria-live="polite"`, `role="status"`, `role="progressbar"`).
  - Telemetry and decorative elements use `aria-hidden="true"`.

## Testing & Verification
- Test interactive flows directly inside the browser canvas using `evaluate_javascript` or standard browser actions:
  - Test keyboard shortcuts across questions.
  - Verify correct animation classes (`.correct`, `.wrong`, `.dimmed`).
  - Check score calculation and results tier emoji output.
