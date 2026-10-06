# Quiz CLI

An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts. The application runs in a terminal, presents multiple-choice questions, explains answers, tracks progress, and displays a final score with incorrect-answer review.

## Features

- Three built-in quiz categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Choose all available questions, or select a three- or five-question quiz when the category contains enough questions.
- Shuffles questions for each quiz.
- Displays a visual progress bar while the quiz is in progress.
- Provides immediate correct/incorrect feedback and explanations.
- Shows the final score, percentage, performance message, and incorrect-answer review.
- Supports replaying without restarting the application.
- Uses only Node.js built-in modules; no runtime dependencies are required.
- Uses ANSI escape codes for terminal styling without an external color package.

## Technology Stack

| Area | Technology |
| --- | --- |
| Runtime | Node.js 18 or newer |
| Language | JavaScript using ES modules |
| Input | Node.js `readline` |
| File loading | Node.js `fs/promises`, `path`, and `url` |
| Data | JSON (`data/questions.json`) |
| Tests | Node.js built-in test runner command (`node --test`) |

## Prerequisites

- Node.js `18.0.0` or newer, as specified by `package.json`.
- A terminal capable of displaying standard ANSI escape codes for the intended colored output.
- npm, which is distributed with Node.js. No package installation is currently required because the project declares no dependencies.

## Installation

Clone the repository and enter its directory:

```bash
git clone <repository-url>
cd <repository-directory>
```

The repository has no declared dependencies, so there is no required `npm install` step. The application can be started directly with Node.js.

## Running the Quiz

Start the application with the defined npm script:

```bash
npm start
```

The equivalent direct command is:

```bash
node index.js
```

Follow the prompts to:

1. Choose a category by entering its menu number.
2. Choose all questions, three questions, or five questions when available.
3. Press Enter to begin.
4. Select an answer for each question by entering its number.
5. Press Enter between questions when prompted.
6. Review the result and choose whether to play again.

To stop the process, use the normal terminal interrupt shortcut, such as `Ctrl+C`.

## Configuration and Question Data

There are no environment variables, configuration files, credentials, or external services required by the application.

Questions are loaded at runtime from `data/questions.json`. The file is organized by category:

```json
{
  "categories": {
    "category-id": {
      "name": "Display name",
      "questions": [
        {
          "question": "Question text",
          "options": ["Option 1", "Option 2"],
          "answer": 0,
          "explanation": "Optional explanation"
        }
      ]
    }
  }
}
```

The `answer` value is a zero-based index into `options`. For example, `"answer": 0` marks the first option as correct. Each category should contain at least one question; the menu only offers three- and five-question choices when the category has at least that many questions.

## How It Works

1. `index.js` loads and parses `data/questions.json`.
2. The application derives the category menu from the keys in `categories`.
3. `src/input.js` handles menus, free-form prompts, confirmation, and pause prompts through Node's `readline` API.
4. A `Quiz` instance in `src/quiz.js` copies and shuffles the selected questions using the Fisher–Yates algorithm.
5. Each answer is recorded, scored, and immediately evaluated.
6. On completion, the quiz calculates the percentage, prints a performance message, and lists incorrect answers for review.

## Project Structure

```text
.
├── data/
│   └── questions.json   # Quiz categories, options, answers, and explanations
├── src/
│   ├── colors.js        # ANSI color and text-style helpers
│   ├── input.js         # Readline interface and prompt utilities
│   └── quiz.js          # Quiz state, scoring, shuffling, and result display
├── index.js             # Application entry point and main interaction loop
├── package.json         # Project metadata, scripts, and Node.js requirement
└── .DS_Store            # macOS filesystem metadata; not used by the application
```

## Testing

The package defines this test command:

```bash
npm test
```

It runs:

```bash
node --test
```

No test files are currently included in the repository, so the command may complete without executing test cases. The repository does not define linting or formatting scripts.

## Build and Deployment

No build step, bundler, Docker configuration, CI workflow, or deployment configuration is present. This is a local Node.js command-line application and is run directly from the repository.

## Development Notes

- The project uses ES module syntax because `package.json` sets `"type": "module"`.
- Keep question answers synchronized with their option arrays: `answer` must refer to an existing zero-based option index.
- The application reads the question file relative to `index.js`, so preserve the `data/questions.json` path unless the loader is updated as well.
- Terminal styling is implemented locally in `src/colors.js`; no color dependency needs to be installed.

## License

The project declares the [MIT License](https://opensource.org/licenses/MIT) in `package.json`.
