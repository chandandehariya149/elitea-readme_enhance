# Quiz CLI

An interactive, dependency-free command-line quiz game for learning JavaScript, Node.js, and general programming concepts.

## Overview

Quiz CLI is a Node.js terminal application that loads quiz content from `data/questions.json`. Players choose a category and the number of questions, answer randomized multiple-choice questions, receive immediate correctness feedback and explanations, and see their progress and final score. At the end of a round, the game reviews incorrect answers and offers the option to play again.

## Features

- Interactive terminal prompts for category and question-count selection
- Three quiz categories included:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Randomized question order using an in-place shuffle
- Multiple-choice questions with zero-based answer indexes in the data file
- Immediate answer feedback and explanations
- Progress bar during a quiz
- Final score and performance feedback
- Review of incorrect answers
- Replay support
- ANSI terminal colors without an external color dependency

## Technology stack

- Node.js 18 or newer
- Native JavaScript ES modules
- Node.js built-in modules, including `fs/promises`, `url`, `path`, and `readline`
- JSON-based question data
- No runtime or development npm dependencies

## Prerequisites

- Node.js `18.0.0` or newer
- An interactive terminal capable of accepting prompts

You can verify your Node.js version with:

```sh
node --version
```

## Installation and setup

Clone the repository and enter its root directory:

```sh
git clone https://github.com/chandandehariya149/elitea-readme_enhance.git
cd elitea-readme_enhance
```

No dependency installation is required because the project has no external npm packages. Running `npm install` is optional and is not needed to use the application.

## Running the quiz

Start the application with the configured npm script:

```sh
npm start
```

Alternatively, run the entry point directly:

```sh
node index.js
```

Follow the prompts to select a category, choose how many questions to answer, and submit an option for each question. The application is designed for an interactive terminal rather than redirected or non-interactive input.

## How a round works

1. The application displays a welcome message and available categories.
2. You select a category and question count.
3. Questions from the selected category are shuffled and presented as multiple choice.
4. Each answer receives immediate feedback, including an explanation from the data file.
5. A progress bar tracks the round.
6. The results screen shows the score and performance message.
7. Incorrect answers are reviewed.
8. You can choose whether to start another round.

Performance feedback is based on the percentage score:

| Score | Feedback |
| --- | --- |
| 100% | Perfect |
| 80–99% | Great |
| 60–79% | Good |
| 40–59% | Room for improvement |
| Below 40% | Keep practicing |

## Project structure

```text
.
├── data/
│   └── questions.json   # Categories and quiz questions
├── src/
│   ├── colors.js        # ANSI styling helpers
│   ├── input.js         # Readline-based prompt utilities
│   └── quiz.js          # Quiz flow, shuffling, scoring, and results
├── index.js             # Application entry point and setup flow
└── package.json         # Project metadata and npm scripts
```

`index.js` resolves the question data relative to the module location, so the application should be launched from a normal checkout with the repository files intact.

## Question data and customization

Quiz content is stored in `data/questions.json`. The top-level value is an object whose keys are category names and whose values are arrays of question objects. Each question uses this schema:

```json
{
  "question": "Which keyword declares a constant in JavaScript?",
  "options": ["var", "let", "const", "static"],
  "answer": 2,
  "explanation": "The const keyword declares a binding that cannot be reassigned."
}
```

To add or customize content:

1. Open `data/questions.json`.
2. Add a new category key or append a question to an existing category array.
3. Provide a `question`, an `options` array, a numeric `answer`, and an `explanation`.
4. Set `answer` to the **zero-based index** of the correct option: `0` for the first option, `1` for the second, and so on.
5. Keep the JSON valid before starting the application.

## Available scripts

| Command | Description |
| --- | --- |
| `npm start` | Runs `node index.js`. |
| `npm test` | Runs Node.js’s test runner with `node --test`. |

## Testing status

The `npm test` script is configured, but the repository currently contains no test files. Running it therefore does not provide application test coverage. The quiz can be verified manually by running `npm start` and exercising category selection, question answering, scoring, incorrect-answer review, and replay.

## Build and deployment

There is no build step, bundler, deployment configuration, or server component. Run the application directly with Node.js from the repository root.

## Notes and limitations

- The quiz requires an interactive terminal because it uses readline prompts.
- Questions are loaded from the local `data/questions.json` file; there is no database, network service, or remote content source.
- Terminal colors use ANSI escape sequences. If a terminal does not support ANSI styling, the quiz remains usable but its colors may not display correctly.
- The included categories currently contain five questions each.

## Contributing

To contribute, make a focused change, keep question data valid JSON, and manually run the quiz to verify the interactive flow. If adding automated tests, ensure they are compatible with the existing `node --test` command.

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), as specified in `package.json`.
