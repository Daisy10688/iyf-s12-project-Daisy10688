# FridgeChef — Cook with What You Have

> **Project proposal and implementation guide**  
> FridgeChef is a practical website that helps people turn the food they already have at home into meal ideas. This document explains the purpose, intended users, features, internal workings, required tools, development process, and how a group can work together to deliver the project.

## 1. Project overview

Many people have ingredients in their fridge or pantry but are unsure what to cook with them. They may search for recipes one ingredient at a time, buy more food than they need, or let ingredients go to waste. FridgeChef addresses this everyday problem by letting a person enter available ingredients and showing recipes that use them.

The first version will be a responsive front-end website built with **HTML, CSS, and vanilla JavaScript**. It will use a small recipe collection stored in the project itself, so the core experience works without a paid service, user account, or server. The site will clearly show which recipe ingredients the person already has and which ingredients are missing.

### Project aim

Build a clear, easy-to-use website that accepts a user's ingredients and returns useful, understandable meal suggestions ranked by how well they match.

### Objectives

- Help users make a meal from ingredients already available at home.
- Reduce the time it takes to decide what to cook.
- Make it clear when a recipe needs ingredients the user does not have.
- Encourage users to use available food and reduce avoidable food waste.
- Create a working project that can be demonstrated in a browser and explained to reviewers.

## 2. Intended users and use case

FridgeChef is intended for anyone who cooks at home, including students, families, busy workers, and people trying to plan meals on a budget. The first version is designed for a person who wants a quick answer, rather than a complex meal-planning system.

**Example:** A user has eggs, tomatoes, onions, and bread. They enter those ingredients. FridgeChef checks its recipe collection and might show tomato-and-egg scramble first, then an omelette, then a recipe that needs one extra ingredient. Each suggestion explains what the user has, what is missing, and how to prepare the meal.

## 3. User journey

1. The user opens the FridgeChef home page.
2. A short instruction explains that ingredients can be entered separately or as a comma-separated list.
3. The user types ingredients such as `eggs, tomatoes, onion` and adds them to the list.
4. The user can inspect the list and remove an item entered by mistake.
5. The user selects **Find recipes**.
6. FridgeChef compares the ingredients with its recipe collection and ranks suitable recipes.
7. Recipe cards show the meal name, a short description, match information, missing ingredients if any, and preparation steps.
8. If there are no results, the site explains why and suggests adding ingredients or allowing recipes with missing ingredients.

## 4. Scope and features

### Included in the first version

- A welcoming page title and short explanation of the site.
- An ingredient input with an add action; comma-separated entry may also be supported.
- A visible list of entered ingredients.
- The ability to remove ingredients from the list.
- Input cleanup: trim extra spaces, ignore capitalization differences, and avoid duplicate entries.
- A **Find recipes** button.
- A local collection of sample recipes stored in JavaScript.
- Recipe matching and ranking based on available ingredients.
- Recipe cards that distinguish available ingredients from missing ones.
- A useful message before the first search, when there are no matches, or when the input is empty.
- A responsive layout for both mobile and desktop screens.
- Basic accessibility: labeled inputs, readable contrast, keyboard-operable controls, and meaningful page structure.

### Optional additions if time allows

- A control to show only recipes with all ingredients, or also show recipes missing one or two.
- Filters for meal type, preparation time, or dietary preference.
- A clear-all button.
- A small set of recipe images or simple food illustrations.
- Saving favorites in the browser with `localStorage`.

### Out of scope for the first version

The first version does not need user registration, a cloud database, online ordering, nutrition advice, or a live recipe API. Those features add complexity and can be considered after the core website works. Recipe suggestions are informational; users should check ingredients and dietary suitability themselves.

## 5. How the website works internally

The initial project has three main parts:

1. **HTML** defines the page: ingredient form, ingredient list, search control, and results area.
2. **CSS** controls the visual design, layout, responsive behavior, and visible states such as ingredient chips and recipe cards.
3. **JavaScript** stores the sample recipes, handles user actions, compares ingredients, ranks matches, and updates the results on the page.

No build system is required for the first version. The browser loads `index.html`, which links to the stylesheet and JavaScript file.

### Recipe data

Each recipe should be represented consistently. For example:

```js
{
  id: "tomato-egg-scramble",
  name: "Tomato and Egg Scramble",
  description: "A quick, filling meal made in one pan.",
  ingredients: ["eggs", "tomatoes", "onion", "oil", "salt"],
  steps: [
    "Chop the tomatoes and onion.",
    "Cook the onion and tomatoes in a pan with a little oil.",
    "Add beaten eggs and stir until cooked. Season to taste."
  ],
  mealType: "breakfast",
  prepMinutes: 15
}
```

For a useful demonstration, the group should agree on a manageable starter collection (for example, 10–20 familiar meals) and make sure every recipe has complete, consistent fields. Ingredients should use simple names that users are likely to type. More advanced ingredient aliases, such as mapping `scallion` to `spring onion`, can be added later.

### Ingredient normalization

Before comparing items, JavaScript should normalize them so harmless differences do not prevent a match. A simple first version can:

- Trim spaces at the start and end.
- Convert text to lowercase for comparison.
- Collapse repeated spaces.
- Ignore empty values.
- Prevent duplicate ingredients from being added.

Keep the display text friendly (for example, “Spring onion”) while using a normalized value (for example, `spring onion`) for comparisons. The initial version can use exact normalized names; handling synonyms or quantities is a possible improvement.

### Matching and ranking

For each recipe, compare its ingredient list with the user's normalized ingredient list. Calculate:

- **Available ingredients:** recipe ingredients found in the user's list.
- **Missing ingredients:** recipe ingredients not found in the user's list.
- **Match percentage:** available recipe ingredients divided by the total recipe ingredients, multiplied by 100.

One simple ranking rule is to sort recipes by fewest missing ingredients first, then by highest match percentage. The interface should make the rule understandable instead of presenting a score without explanation. In a first version, recipes with all required ingredients can appear before recipes missing one or two. Recipes missing too many items can be hidden or shown only when the user chooses to allow extra ingredients.

The result calculation can follow this outline:

```text
for each recipe:
    available = recipe ingredients that appear in user's ingredient set
    missing = recipe ingredients that do not appear in user's ingredient set
    match percentage = available count / recipe ingredient count * 100

keep recipes that meet the chosen missing-ingredient limit
sort by fewest missing ingredients, then highest match percentage
render the ranked recipes
```

The score is a practical guide, not a measure of taste or nutrition. A later version might distinguish essential ingredients from pantry staples such as salt, water, and cooking oil so that these do not unfairly lower a recipe's match.

### Displaying results safely

JavaScript should create result elements and place user-provided text into them as text content. This avoids interpreting entered ingredients as HTML. Each recipe card should include:

- Recipe name and brief description.
- A clear match summary, such as “You have 4 of 5 ingredients.”
- Ingredients the user has.
- Ingredients still needed, if any.
- Preparation steps.
- Optional preparation time or meal type, if available.

The page should update its results area after a search without requiring a full reload.

## 6. Tools and materials needed

### Required tools

- **A code editor:** Visual Studio Code is a suitable free option. Any editor that can edit plain text files will work.
- **A modern web browser:** Chrome, Edge, Firefox, or Safari for running and reviewing the site.
- **HTML:** page structure and content.
- **CSS:** appearance and responsive layout.
- **JavaScript:** ingredient input, matching, ranking, and result rendering.
- **GitHub:** shared repository for the source files, README, issues, and version history.
- **Git:** version control for tracking changes and combining group work. GitHub Desktop can be used by members who prefer a graphical interface.
- **A way to create the requested PDF:** GitHub's rendered README can be printed to PDF from a browser, or the Markdown file can be opened in an editor that supports PDF export. Review the exported pages before submitting.

### Helpful, but not required

- **Live Server** editor extension, for automatically refreshing the website while editing. Alternatively, open `index.html` directly in the browser.
- **A simple wireframe tool** such as paper and pen, Figma, or a drawing app to agree on the page layout before implementation.
- **GitHub Issues or a shared task board** to assign tasks and track progress.
- **A shared document or group chat** for decisions, meeting notes, and updates.

The project does not require Node.js, a framework, a paid API, or a database for the first version.

## 7. Suggested repository structure

```text
fridgechef/
├── index.html          # Main page and semantic structure
├── styles.css          # Colors, typography, layout, and responsive rules
├── script.js           # Recipe data, ingredient controls, matching, and rendering
├── README.md           # Project explanation, instructions, and team information
└── assets/             # Optional local images or icons, if used
```

Keep filenames lowercase and use clear names. If the project grows, JavaScript can later be split into files such as `recipes.js` and `matching.js`, but a small first version can remain in `script.js`.

## 8. Step-by-step development plan

### Step 1: Agree on the project brief

As a group, confirm the problem FridgeChef solves, the first-version features, the intended users, and the deadline. Agree which optional features will be postponed so the team can finish a complete working core experience.

### Step 2: Create and organize the GitHub repository

Create a repository named `fridgechef`. Add this README and the initial project files. Add all group members as collaborators if appropriate. Make sure everyone can access the repository and knows how to make a change and share it.

### Step 3: Plan the user interface

Sketch the page before coding. Decide where the title, ingredient entry, ingredient list, search button, result cards, and empty-state messages will go. Review the sketch as a group and agree on colors, typography, and the general look.

### Step 4: Define the recipe collection

Choose familiar recipes and record each one in the same format. Check spelling and consistency in ingredient names. Include practical instructions and avoid adding a recipe unless the group can explain its ingredients and steps.

### Step 5: Build the HTML structure

Create the page sections and form controls in `index.html`. Use meaningful headings, labels, buttons, and sections. Link `styles.css` and `script.js`. Make the page understandable before styling is applied.

### Step 6: Add the visual design

Write CSS for the page layout, typography, buttons, ingredient chips, and recipe cards. Add responsive rules so controls and text fit on a phone as well as a wider screen. Maintain readable contrast and visible keyboard focus.

### Step 7: Implement ingredient entry

Use JavaScript to handle the form submission. Accept one ingredient at a time, and optionally split comma-separated text. Normalize values for comparison, reject empty entries, avoid duplicates, update the visible list, and allow individual items to be removed.

### Step 8: Implement recipe matching

Represent recipes as JavaScript data. On search, normalize the user's ingredient list, calculate the available and missing ingredients for every recipe, apply the agreed matching threshold, and sort results using the agreed ranking rule.

### Step 9: Render cards and messages

Display recipes in a consistent card layout. Show why a recipe matched and which ingredients are missing. Add clear messages for the initial page, an empty ingredient list, and searches with no suitable results. Use safe text insertion for ingredient names.

### Step 10: Review, fix, and prepare the submission

Have another team member try the website using the scenarios in the checklist below. Fix confusing interactions and visual issues. Update this README with the team's final implementation details, then export or print the README as a PDF if a PDF is required. Open the PDF and confirm that headings, code samples, and page breaks are readable before sending it.

## 9. Working as a group

Good group work means agreeing on the shared goal, splitting work into clear pieces, sharing progress, and integrating everyone's changes before the deadline. Assign roles based on the number and strengths of team members. One person can take more than one role in a small group.

### Suggested roles

- **Coordinator / project lead:** keeps the task list current, checks the deadline, schedules short check-ins, and makes sure decisions are recorded. This role does not mean one person must do all the coding.
- **Design and HTML lead:** prepares the wireframe and builds the page structure and accessible form controls.
- **CSS and responsive design lead:** creates the visual style and checks the layout on phone and desktop sizes.
- **JavaScript and recipe-data lead:** implements ingredient entry, recipe data, matching, ranking, and result display.
- **Documentation and review lead:** keeps the README accurate, checks that setup instructions work, coordinates feedback, and prepares the PDF submission.

If there are fewer members, combine roles. All team members should understand the complete user journey and review the final project together.

### Team habits

1. Agree on filenames, recipe data shape, ingredient naming, and matching rules before parallel coding begins.
2. Write down each task, who owns it, and when it should be ready.
3. Share short updates regularly: what is finished, what is next, and what is blocked.
4. Make small, focused changes and commit them with messages that explain the change.
5. Avoid having multiple people edit the same file at the same time where possible. If that is necessary, coordinate first and resolve conflicts together.
6. Review changes before merging them into the main branch. Check that the page still loads and that the related feature works.
7. Keep the main branch in a usable state. Add unfinished ideas to the task list instead of leaving broken code in the main version.
8. Make sure every member can explain their contribution and the project's overall behavior for the presentation or review.

### Simple GitHub collaboration workflow

1. Keep the shared, reviewed version on the `main` branch.
2. For a task, create a short branch such as `feature/ingredient-input` or `style/recipe-cards`.
3. Make focused changes and commit them with a clear message, such as `Add ingredient entry and removal`.
4. Push the branch to GitHub and open a pull request describing what changed and how it can be reviewed.
5. Ask a teammate to review the changes. Address feedback and resolve conflicts if they occur.
6. Merge the pull request when it is ready, then update local copies before starting the next task.

Members who are new to Git can use GitHub Desktop to create branches, commit, push, and open pull requests. The team should choose one workflow and use it consistently.

## 10. Example three-day work plan

The exact timing can be adjusted, but the plan below helps the group deliver a complete explanation and a working first version within a short deadline.

### Day 1 — Plan and establish the foundation

- Confirm the problem, audience, must-have features, and limits of the first version.
- Create the repository, project files, and task list.
- Agree on the page sketch, visual direction, recipe object format, and match rule.
- Build the basic HTML structure and add a starter set of recipes.
- Draft the project explanation and gather any information needed for the PDF.

**End-of-day result:** a clear agreed plan, accessible shared repository, page skeleton, and recipe data outline.

### Day 2 — Implement the main experience

- Add ingredient entry, normalization, duplicate prevention, and removal.
- Implement recipe comparison, ranking, and result cards.
- Style the main page and make it usable on small screens.
- Combine work through reviewed branches or coordinated commits.
- Have a teammate who did not build a feature try it and report issues.

**End-of-day result:** the main user journey works from entering ingredients to reading recipe suggestions.

### Day 3 — Review, polish, and submit

- Fix issues found during review and check the key scenarios.
- Confirm page text, recipe data, links, and setup instructions.
- Update the README so it describes what the project actually contains.
- Export or print the README to PDF as requested, then inspect the PDF pages.
- Confirm the repository and required files are ready and submit the requested materials before the deadline.

**End-of-day result:** a presentable, working first version and a reviewed project explanation PDF.

## 11. Review checklist

Use this checklist before showing or submitting the project:

- [ ] The page opens in a modern browser without requiring a build step.
- [ ] A user can add one ingredient and see it in the list.
- [ ] Comma-separated entry works if the team chose to support it.
- [ ] Empty values and duplicate ingredients are handled sensibly.
- [ ] A user can remove an ingredient.
- [ ] Searches with common ingredients show relevant recipes.
- [ ] Available and missing ingredients are clearly distinguished.
- [ ] Recipes are ordered according to the documented matching rule.
- [ ] Empty input and no-match searches show helpful explanations.
- [ ] Buttons and inputs work with a keyboard and have clear labels.
- [ ] Text and controls remain readable on a phone-sized screen.
- [ ] The README matches the current project and explains how to run it.
- [ ] The exported PDF is readable and includes the complete project explanation.

## 12. Known limitations and possible next steps

The first version uses a small, manually maintained recipe list. It will not recognize every spelling variation, ingredient synonym, brand name, quantity, or substitution. Its match score only compares names and does not judge whether the amounts are sufficient. It also does not verify allergies or dietary safety. These limits should be explained honestly during a demonstration.

After the first version is complete, the project could be improved by:

- Supporting ingredient aliases and common spelling variations.
- Separating pantry staples from ingredients that are central to a recipe.
- Adding dietary and meal-type filters.
- Adding cooking time and difficulty information.
- Letting users save favorites in their browser.
- Storing recipes in a JSON file or database as the collection grows.
- Connecting to a recipe API, after reviewing its cost, licensing, reliability, and data requirements.
- Adding automated checks for ingredient matching and input edge cases.

## 13. Running the project

For the initial front-end version:

1. Download or clone the repository.
2. Open `index.html` directly in a modern web browser, or open the project folder in an editor and use a local preview extension such as Live Server.
3. Enter several ingredients and select **Find recipes**.

No package installation or server is required unless the team later chooses to add one.

## 14. License and attribution

No license has been selected for this project yet. If the group plans to share or reuse the code publicly, agree on an appropriate license and add a `LICENSE` file. If images, icons, recipe text, or other material come from an external source, record the source and check its permission and attribution requirements before including it.
