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
