# Quiz CLI

Quiz CLI is an interactive terminal quiz game built with Node.js and ECMAScript modules. It helps users test programming knowledge through multiple-choice questions, immediate feedback, explanations, progress tracking, and final score review.

The question bank currently contains 15 questions across JavaScript Basics, Node.js Fundamentals, and General Programming.

## Features

- Interactive terminal-based menus with numeric input validation
- Three programming-focused categories
- Choice of all available questions, 3 questions, or 5 questions when enough questions exist
- Randomized question order for each quiz
- Immediate correct/incorrect feedback
- Explanations for questions that provide them
- Visual progress bar and question counter
- Final score and percentage with performance feedback
- Review of incorrect answers
- Option to play again
- ANSI terminal colors implemented without external dependencies

## Technology stack

- Node.js 18 or newer
- JavaScript using ECMAScript modules (`"type": "module"`)
- Node.js built-in `readline`, filesystem, URL, and path APIs
- JSON question data
- Node.js built-in test runner command (`node --test`)
- No runtime or development dependencies

## Prerequisites

Install [Node.js](https://nodejs.org/) 18 or newer. The required version is declared in `package.json` as `>=18.0.0`.

## Installation

Clone the repository and change into its directory:

```bash
git clone https://github.com/chandandehariya149/elitea-readme_enhance.git
cd elitea-readme_enhance
```

This project has no dependencies, so `npm install` is not required. Running it is harmless if you prefer to initialize the local npm environment:

```bash
npm install
```

## Running the quiz

Start the game with:

```bash
npm start
```

Alternatively, run the entry point directly:

```bash
node index.js
```

The application will ask you to:

1. Choose a category.
2. Choose all questions, 3 questions, or 5 questions when that option is available.
3. Press Enter to begin.
4. Select each answer by entering its displayed number.
5. Press Enter between questions when prompted.
6. Review your score and any incorrect answers.
7. Choose whether to play again.

## Categories

| Category | Questions |
| --- | ---: |
| JavaScript Basics | 5 |
| Node.js Fundamentals | 5 |
| General Programming | 5 |

## Question data format

Questions are stored in `data/questions.json`. The top-level `categories` object maps category IDs to category records. Each question uses this schema:

```json
{
  "question": "What keyword is used to declare a constant in JavaScript?",
  "options": ["var", "let", "const", "define"],
  "answer": 2,
  "explanation": "The 'const' keyword declares a block-scoped constant that cannot be reassigned."
}
```

- `question`: The question text.
- `options`: An array of answer choices displayed to the player.
- `answer`: A zero-based index into `options`; `0` identifies the first option.
- `explanation`: Optional explanatory text shown after the answer.

When adding questions, keep `answer` aligned with the zero-based position of the correct option.

## Project structure

```text
.
├── data/
│   └── questions.json   # Categories and question bank
├── src/
│   ├── colors.js        # ANSI color and style helpers
│   ├── input.js         # readline prompts, menus, and confirmations
│   └── quiz.js          # Quiz state, shuffling, scoring, and results
├── index.js             # Application entry point and main game loop
└── package.json         # Project metadata and npm scripts
```

## Architecture

- `index.js` loads `data/questions.json`, creates the readline interface, presents the category and question-count menus, runs the main replay loop, and handles top-level errors.
- `src/input.js` wraps Node.js `readline` in promise-based helpers for prompts, numbered selections, yes/no confirmation, and pause prompts.
- `src/quiz.js` owns quiz state. It shuffles a copy of the selected questions with Fisher–Yates, tracks progress and score, records answers, displays feedback, and renders final results and incorrect-answer review.
- `src/colors.js` provides ANSI escape-code styling helpers used by the terminal output.

## Testing

The package defines:

```bash
npm test
```

This runs `node --test`. There are currently no test files in the repository, so the command does not execute project-specific test cases.

## Development notes

- The project uses native ECMAScript module syntax (`import`/`export`) and does not use a transpiler or bundler.
- Questions are loaded at runtime from `data/questions.json` relative to the entry-point file, so the data file must remain in that location unless the loader is changed.
- The game shuffles the selected questions, but answer options remain in the order stored in the JSON file.
- Numeric menu input is validated and reprompted until it falls within the displayed range.
- Terminal styling uses ANSI escape sequences and has no external package dependency.

## Build and deployment

No build script, bundler configuration, Docker configuration, or deployment configuration is included. Run the application directly with Node.js on a terminal; no separate build step is required.

## Limitations

- The question bank is local JSON data and is not backed by a database or external service.
- There is no persistent score history, user account system, network API, or automated test suite currently included.
- The available question-count choices are based on the number of questions in the selected category: all questions is always available, while 3 and 5 questions are shown only when enough questions exist.

## Contributing

To modify the quiz locally:

1. Edit the source files or add questions to `data/questions.json`.
2. Preserve the question schema and zero-based answer indexes.
3. Run `npm test` to execute the configured Node.js test command.
4. Run `npm start` to verify the interactive flow manually.

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), as declared in `package.json`.
```
