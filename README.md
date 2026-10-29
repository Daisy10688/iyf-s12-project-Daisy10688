# FridgeChef

FridgeChef is a simple, practical website that helps people decide what to cook with ingredients they already have at home. A user enters the ingredients in their fridge or pantry, and the site suggests recipes they can make, including recipes that need only a few extra ingredients.

The first version will be built with **HTML, CSS, and vanilla JavaScript**. It can run directly in a web browser without a server or account.

## Project goals

- Make it quick to turn a list of ingredients into meal ideas.
- Show which ingredients a recipe uses and which ones are missing.
- Keep the interface clear and usable on phones and computers.
- Start with a small, editable recipe collection, then expand it over time.

## First version features

1. An input where users can add ingredients, one at a time or as a comma-separated list.
2. A visible ingredient list with a way to remove items.
3. A **Find recipes** action that compares the user's ingredients with the recipe collection.
4. Recipe cards showing the meal name, description, available ingredients, missing ingredients, and basic cooking steps.
5. A helpful empty state when there are no matches, with an option to allow recipes that need extra ingredients.
6. A responsive layout and simple input validation.

## How recipe matching works

Each recipe has a list of required ingredients. JavaScript compares that list with the user's ingredients, ignoring differences in capitalization and extra spaces. Recipes can be ranked by how many required ingredients are available. The results should clearly distinguish ingredients the user has from ingredients they still need.

For the first version, recipes can live in a JavaScript array. This keeps the project self-contained and makes it easy to add or edit recipes. A future version could use a recipe API or a database.

## Suggested project files

```text
fridgechef/
├── index.html       # Page structure and content
├── styles.css       # Layout, colors, and responsive design
├── script.js        # Ingredient input and recipe matching
└── README.md        # Project overview and build instructions
```

## Steps to create the project

### 1. Set up the folder

Create a folder named `fridgechef` and add `index.html`, `styles.css`, and `script.js`. Add this README to document the project.

### 2. Plan the page

Sketch a simple page with a title and short introduction, an ingredient entry area, the user's ingredient list, a search button, and a section for recipe results. Decide how the page will look when the user has not searched yet or when there are no matches.

### 3. Build the HTML

In `index.html`, create semantic sections for the header, ingredient form, ingredient list, and recipe results. Add labels to form controls and load `styles.css` and `script.js` from the page.

### 4. Style the page with CSS

In `styles.css`, choose a friendly food-inspired color palette, readable fonts, and clear spacing. Style ingredient chips and recipe cards, then add a small-screen layout with a CSS media query.

### 5. Add an initial recipe collection

In `script.js`, define a small set of sample recipes. Give each recipe a name, description, ingredient list, and simple preparation instructions. Use common ingredients so the first search is useful.

### 6. Implement ingredient entry

Use JavaScript to read the form, trim whitespace, normalize capitalization for comparisons, and add ingredients to the visible list. Support removing an ingredient and prevent empty or duplicate entries. If accepting comma-separated input, split it into individual ingredients.

### 7. Match ingredients to recipes

When the user searches, compare their ingredient list with each recipe. Calculate which ingredients are available and which are missing, then show the strongest matches first. Make the matching rule clear—for example, show recipes with all ingredients first, followed by recipes missing one or two.

### 8. Render the results

Build a recipe card for each match using DOM elements and text content. Show the recipe name, available ingredients, missing ingredients (if any), and preparation steps. Display a helpful message if no recipes meet the selected matching rule.

### 9. Check usability

Try the page with an empty input, one ingredient, several comma-separated ingredients, duplicate ingredients, and ingredients that produce no matches. Check that controls have labels, results are easy to scan, and the layout works at phone width.

### 10. Add recipes and improve it

Grow the sample collection and refine the design based on feedback. Possible later additions include saving favorite recipes, dietary filters, ingredient suggestions, and connecting to a recipe service.

## Running the project

Once the three front-end files are in place, open `index.html` in a modern web browser. No build tools or package installation are required for the initial version.

## Future ideas

- Dietary preferences such as vegetarian or dairy-free.
- Search by meal type or cooking time.
- Save favorite recipes in the browser.
- Let users choose whether to include recipes with missing ingredients.
- Use a recipe API for a larger collection.

## License

No license has been selected yet. Add one if the project will be shared or reused publicly.
