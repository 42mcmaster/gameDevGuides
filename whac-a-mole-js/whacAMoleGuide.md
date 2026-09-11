# Whac-a-Mole in JavaScript — Build Guide

This guide goes with the **Kenny Yip Coding** video: [Whac a Mole in JavaScript](https://youtu.be/ej8SatOj3V4). You will build a Whac-a-Mole game using HTML, CSS, and JavaScript in VS Code, and play it in your web browser.

In the game, a mole and a piranha plant pop out of nine pipes. Click the mole to score points. Click the plant and the game is over. You can [play the finished game here](https://imkennyyip.github.io/whac-a-mole/).

**What you will learn**

- How JavaScript changes a web page while it is open
- **Variables**, **functions**, **if statements**, and **loops**
- How to make **random numbers**
- How to run code on a **timer**
- How to make something happen when you **click**

**How to use this guide**

1. Watch one part of the video.
2. Build that part. Read the steps and hints in this guide.
3. Try it on your own first. If you are stuck, open the **"Stuck? Click to see the code"** section for that part.
4. At each **Checkpoint**, save, refresh your browser, and make sure it works before you move on.

---

## Table of Contents

- [Before You Start](#before-you-start)
- [Reading JavaScript Code](#reading-javascript-code)
- [Part 1: Build the HTML Page](#part-1-build-the-html-page)
- [Part 2: Style the Page](#part-2-style-the-page)
- [Part 3: Style the Game Board](#part-3-style-the-game-board)
- [Part 4: Create the Nine Tiles](#part-4-create-the-nine-tiles)
- [Part 5: Style the Tiles](#part-5-style-the-tiles)
- [Part 6: Make the Mole Appear](#part-6-make-the-mole-appear)
- [Part 7: Resize the Mole and Clear the Old Tile](#part-7-resize-the-mole-and-clear-the-old-tile)
- [Part 8: Add the Piranha Plant](#part-8-add-the-piranha-plant)
- [Part 9: Keep the Mole and Plant Apart](#part-9-keep-the-mole-and-plant-apart)
- [Part 10: Click the Tiles and Keep Score](#part-10-click-the-tiles-and-keep-score)
- [Part 11: Stop the Game After Game Over](#part-11-stop-the-game-after-game-over)
- [Part 12: Stop the Images From Being Dragged](#part-12-stop-the-images-from-being-dragged)
- [Use Your Own Images](#use-your-own-images)
- [Troubleshooting](#troubleshooting)
- [Try This Next](#try-this-next)
- [Key Terms](#key-terms)

---

## Before You Start

### Set up your project folder

1. On GitHub, create a new repo named `Games`. Open it in VS Code the way you normally open your repos.
2. Inside the `Games` repo, make a folder named `whac-a-mole`. You will add more games to this repo later, each in its own folder.
3. In the `whac-a-mole` folder, create three empty files: `index.html`, `mole.css`, and `mole.js`.

### Get the images

The video tells you to download the images from GitHub.  Those can be downloaded here: https://github.com/ImKennyYip/whac-a-mole. 

You can also make your own images in Piskel. See [Use Your Own Images](#use-your-own-images).

### How to run your game

Open your `whac-a-mole` folder in File Explorer and double-click `index.html`. It opens in your web browser.

Every time you change your code:

1. **Save** the file in VS Code (**Ctrl+S**).
2. **Refresh** the browser (**F5**).

If you forget to save, the browser will not show your change.

### Rules that will save you time

- **JavaScript is case sensitive.** `getElementById` works. `getElementByID` and `getelementbyid` do not.
- **File names must match exactly.** If your code says `monty-mole.png`, the file must be named `monty-mole.png`.
- **Quotes and brackets come in pairs.** Every `(` needs a `)`, every `{` needs a `}`, and every `"` needs another `"`.

---

## Reading JavaScript Code

You already know HTML and CSS. Here is how the three work together:

- **HTML** is what is on the page (headings, divs, images).
- **CSS** is how it looks (colors, sizes, positions).
- **JavaScript** is what it does (moving the mole, counting the score, reacting to clicks).

These pieces show up all through the game:

| Code | What it means |
|---|---|
| `let score = 0;` | Make a variable named `score` that starts at 0 |
| `score += 10;` | Add 10 to `score` |
| `function setMole() { ... }` | Make a function (a named set of steps) called `setMole` |
| `setMole();` | Run the `setMole` function |
| `if (gameOver) { ... }` | If `gameOver` is true, run the code in the braces |
| `==` | Check if two things are equal |
| `&&` | And |
| `// comment` | A note for people. The computer ignores it. |
| `document.getElementById("score")` | Find the HTML element with `id="score"` |

---

## Part 1: Build the HTML Page

**File:** `index.html`

**What to build**

1. The basic HTML page structure with a `<head>` and `<body>`.
2. In the `<head>`:
   - a `<title>`
   - a `<link>` to `mole.css`
   - a `<script>` that loads `mole.js`
3. In the `<body>`:
   - an `<h1>` with the name of the game
   - an `<h2>` with `id="score"` and the text `0`
   - an empty `<div>` with `id="board"`

**Hints**

- In VS Code, type `!` in an empty HTML file and press **Enter**. VS Code fills in the basic page structure for you.
- The `id` is how JavaScript will find these elements later. Spell them exactly: `score` and `board`.
- The board `<div>` stays empty. JavaScript will fill it with nine tiles.

<details>
<summary>Stuck? Click to see the code</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Whac a Mole</title>
    <link rel="stylesheet" href="mole.css">
    <script src="mole.js"></script>
</head>
<body>
    <h1>Whac a Mole</h1>
    <h2 id="score">0</h2>
    <!-- the game board: JavaScript will fill this with 9 tiles -->
    <div id="board">
    </div>
</body>
</html>
```

</details>

**✅ Checkpoint:** Open `index.html` in your browser. You should see the game name and a `0`.

---

## Part 2: Style the Page

**File:** `mole.css`

**What to build**

Style the `body`:

- font: Arial
- center the text
- background image: `mario-bg.jpg`
- make the background image cover the whole page

**Hints**

- A background image uses `url("./mario-bg.jpg")`. The `./` means "in this same folder."
- `background-size: cover;` stretches the image to fill the page.

<details>
<summary>Stuck? Click to see the code</summary>

```css
body {
    font-family: Arial, Helvetica, sans-serif;
    text-align: center;
    background: url("./mario-bg.jpg");
    background-size: cover;
}
```

</details>

**✅ Checkpoint:** Save and refresh. The page has the background image, and the text is centered.

---

## Part 3: Style the Game Board

**File:** `mole.css`

**What to build**

Style the board. Use `#board` to select the element with `id="board"`.

1. Make it **540px** wide and **540px** tall.
2. Give it a green background color for now, so you can see it.
3. Center it on the page.
4. Use **flexbox with wrapping**, so the tiles you add later line up in rows.
5. Then replace the green with the `soil.png` image, and add a **3px solid white border** with **rounded corners** (25px).

**Hints**

- `margin: 0 auto;` centers a box on the page.
- `display: flex;` and `flex-wrap: wrap;` make the tiles fill left to right, then wrap to the next row. This is what makes a 3 x 3 grid.
- Rounded corners use `border-radius`.

<details>
<summary>Stuck? Click to see the code</summary>

This is the finished version, after the green is replaced with the soil image.

```css
#board {
    width: 540px;
    height: 540px;

    margin: 0 auto;      /* center the board */
    display: flex;       /* tiles line up in a row... */
    flex-wrap: wrap;     /* ...and wrap to the next row */

    background: url("./soil.png");
    background-size: cover;
    border: 3px solid white;
    border-radius: 25px;
}
```

</details>

**✅ Checkpoint:** A square board with a soil background, a white border, and rounded corners sits in the middle of the page.

---

## Part 4: Create the Nine Tiles

**File:** `mole.js`

This is where JavaScript starts. Instead of typing nine `<div>` tags into the HTML, you will use a loop to make them.

**What to build**

1. Use `window.onload` to run a function called `setGame` when the page finishes loading.
2. Write the `setGame` function. Inside it, use a `for` loop that runs 9 times. Each time through the loop:
   - create a new `div`
   - give it an `id` from `"0"` to `"8"`
   - put it inside the board

**Hints**

- `document.createElement("div")` makes a new div in JavaScript.
- `tile.id = i.toString();` gives the tile an id. `toString()` turns the number into text.
- `document.getElementById("board").appendChild(tile);` puts the tile inside the board.
- `for (let i = 0; i < 9; i++)` counts from 0 to 8. It stops before 9.

**Why `window.onload`?** Your `<script>` tag is in the `<head>`, so the JavaScript loads *before* the board exists. `window.onload` waits until the whole page is loaded, so the board is there when your code looks for it.

**Why give each tile an id?** Later, the game needs to know which tile has the mole and which tile you clicked. The ids `0` through `8` tell the tiles apart.

<details>
<summary>Stuck? Click to see the code</summary>

```javascript
window.onload = function() {
    setGame();
}

function setGame() {
    // set up the grid in the html: 9 tiles
    for (let i = 0; i < 9; i++) { // i goes from 0 to 8, stops at 9
        let tile = document.createElement("div");            // make a <div>
        tile.id = i.toString();                              // give it an id "0" to "8"
        document.getElementById("board").appendChild(tile);  // put it inside the board
    }
}
```

</details>

**✅ Checkpoint:** When you refresh, the page looks the same. To see the tiles, right-click the board and choose **Inspect**. Inside `<div id="board">` you should see nine `<div>` tags with ids 0 through 8.

---

## Part 5: Style the Tiles

**File:** `mole.css`

**What to build**

Style every `div` inside the board:

- **180px** wide and **180px** tall
- background image: `pipe.png`, covering the whole tile

**Hints**

- `#board div` selects every div inside the board.
- Why 180? The board is 540px, and the game is 3 tiles across. 540 ÷ 3 = 180.

<details>
<summary>Stuck? Click to see the code</summary>

```css
#board div {
    /* board is 540 x 540, split into 3 x 3 tiles --> 180 x 180 per tile */
    width: 180px;
    height: 180px;
    background-image: url("./pipe.png");
    background-size: cover;
}
```

</details>

**✅ Checkpoint:** You see nine pipes in a 3 x 3 grid.

---

## Part 6: Make the Mole Appear

**File:** `mole.js`

**What to build**

1. At the **top** of the file, make a variable called `currMoleTile`. It will remember which tile has the mole.
2. Write a function called `getRandomTile` that returns a random tile id from `"0"` to `"8"`.
3. Write a function called `setMole` that:
   - creates an `img` element
   - sets its `src` to `./monty-mole.png`
   - gets a random tile id
   - finds that tile and puts the mole image inside it
4. In `setGame`, after the loop, use `setInterval` to run `setMole` every 2 seconds.

**Hints**

- `Math.random()` gives a random decimal from 0 up to (but not including) 1.
- `Math.random() * 9` gives a decimal from 0 up to 9.
- `Math.floor(...)` rounds down, giving a whole number from 0 to 8.
- `setInterval(setMole, 2000);` runs `setMole` every 2000 milliseconds (2 seconds). Write `setMole` with **no** parentheses here, because you are telling `setInterval` which function to run, not running it yourself.

<details>
<summary>Stuck? Click to see the code</summary>

At the top of `mole.js`:

```javascript
let currMoleTile;
```

In `setGame`, after the loop:

```javascript
    setInterval(setMole, 2000); // 2000 milliseconds = 2 seconds
```

Below `setGame`:

```javascript
function getRandomTile() {
    // Math.random() --> 0 to 1 --> times 9 --> 0 to 9 --> round down --> 0 to 8
    let num = Math.floor(Math.random() * 9);
    return num.toString();
}

function setMole() {
    let mole = document.createElement("img");   // make an <img>
    mole.src = "./monty-mole.png";              // show the mole picture

    let num = getRandomTile();
    currMoleTile = document.getElementById(num); // find the random tile
    currMoleTile.appendChild(mole);              // put the mole in it
}
```

</details>

**✅ Checkpoint:** A mole appears in a random pipe. It is too big, and more moles keep piling up. You fix both in the next part.

---

## Part 7: Resize the Mole and Clear the Old Tile

**What to build**

1. **File:** `mole.css`. Make every image inside a tile **100px** wide and **100px** tall.
2. **File:** `mole.js`. At the **start** of `setMole`, clear the tile the mole was in before.

**Hints**

- `#board div img` selects every image inside a tile.
- `currMoleTile.innerHTML = "";` removes everything inside that tile.
- The very first time `setMole` runs, there is no old tile yet. Wrap the clearing line in `if (currMoleTile) { ... }` so it only runs when there is an old tile.

<details>
<summary>Stuck? Click to see the code</summary>

In `mole.css`:

```css
#board div img {
    /* all images inside the tiles */
    width: 100px;
    height: 100px;
}
```

In `mole.js`, at the start of `setMole`:

```javascript
    if (currMoleTile) {
        currMoleTile.innerHTML = "";   // clear the old tile
    }
```

</details>

**✅ Checkpoint:** One smaller mole hops from pipe to pipe.

---

## Part 8: Add the Piranha Plant

**File:** `mole.js`

The plant works almost exactly like the mole.

**What to build**

1. At the top, add a variable called `currPlantTile`.
2. Write a function called `setPlant`. It is the same as `setMole`, but it uses `currPlantTile` and `piranha-plant.png`.
3. In `setGame`, use `setInterval` to run `setPlant`.
4. Set the speeds: the mole every **1 second** (1000) and the plant every **2 seconds** (2000).

**Hints**

- Copy your `setMole` function, paste it, and change the names. Be careful to change **every** `mole` and `currMoleTile` in the copy.
- In the video, he first tries 3000 for the plant, then settles on 1000 for the mole and 2000 for the plant.

<details>
<summary>Stuck? Click to see the code</summary>

At the top of `mole.js`:

```javascript
let currPlantTile;
```

In `setGame`, the two timer lines:

```javascript
    setInterval(setMole, 1000);  // every 1 second
    setInterval(setPlant, 2000); // every 2 seconds
```

Below `setMole`:

```javascript
function setPlant() {
    if (currPlantTile) {
        currPlantTile.innerHTML = "";
    }
    let plant = document.createElement("img");
    plant.src = "./piranha-plant.png";

    let num = getRandomTile();
    currPlantTile = document.getElementById(num);
    currPlantTile.appendChild(plant);
}
```

</details>

**✅ Checkpoint:** The mole and the plant both hop around. Sometimes they land in the same pipe. You fix that next.

---

## Part 9: Keep the Mole and Plant Apart

**File:** `mole.js`

**What to build**

1. In `setMole`, right after you get the random number, check: if the plant is already in that tile, stop and do nothing this time.
2. Do the same in `setPlant`: if the mole is already in that tile, stop.

**Hints**

- `return;` ends a function early.
- Check two things with `&&`: that there is a plant tile, **and** that its id matches the random number.
- `currPlantTile.id == num` checks if the plant's tile is the same tile.

<details>
<summary>Stuck? Click to see the code</summary>

In `setMole`, after `let num = getRandomTile();`:

```javascript
    if (currPlantTile && currPlantTile.id == num) {
        return;   // the plant is already there, so skip this turn
    }
```

In `setPlant`, after `let num = getRandomTile();`:

```javascript
    if (currMoleTile && currMoleTile.id == num) {
        return;   // the mole is already there, so skip this turn
    }
```

</details>

**✅ Checkpoint:** The mole and plant never share a pipe. Sometimes only one of them shows up. That is expected: when they would land on the same tile, one skips its turn.

---

## Part 10: Click the Tiles and Keep Score

**File:** `mole.js`

**What to build**

1. At the top, add two variables: `score` (starts at 0) and `gameOver` (starts at `false`).
2. In the `setGame` loop, add a **click event listener** to each tile that runs a function called `selectTile`.
3. Write `selectTile`:
   - If the clicked tile is the mole's tile, add 10 to the score and show the new score.
   - Otherwise, if the clicked tile is the plant's tile, show `GAME OVER:` and the score, and set `gameOver` to `true`.

**Hints**

- `tile.addEventListener("click", selectTile);` means "when this tile is clicked, run `selectTile`." Put it in the loop, before the tile is added to the board.
- Inside `selectTile`, the word `this` means **the tile that was clicked**.
- `document.getElementById("score").innerText = ...` changes the text of the score heading.

<details>
<summary>Stuck? Click to see the code</summary>

At the top of `mole.js`:

```javascript
let score = 0;
let gameOver = false;
```

In the `setGame` loop, after the `tile.id` line:

```javascript
        tile.addEventListener("click", selectTile);  // run selectTile when clicked
```

At the bottom of the file:

```javascript
function selectTile() {
    if (this == currMoleTile) {              // clicked the mole
        score += 10;
        document.getElementById("score").innerText = score.toString();
    }
    else if (this == currPlantTile) {        // clicked the plant
        document.getElementById("score").innerText = "GAME OVER: " + score.toString();
        gameOver = true;
    }
}
```

</details>

**✅ Checkpoint:** Clicking the mole adds 10 points. Clicking the plant shows GAME OVER. But the mole and plant keep moving, and you can still score. You fix that next.

---

## Part 11: Stop the Game After Game Over

**File:** `mole.js`

**What to build**

At the start of `setMole`, `setPlant`, and `selectTile`, add a check: if the game is over, stop the function right away.

**Hints**

- This is the same `return;` trick from Part 9.
- It must be the **first** thing in each function.

<details>
<summary>Stuck? Click to see the code</summary>

Add this as the first lines inside `setMole`, `setPlant`, and `selectTile`:

```javascript
    if (gameOver) {
        return;
    }
```

</details>

**✅ Checkpoint:** After you click the plant, the mole and plant freeze, and clicking does nothing.

---

## Part 12: Stop the Images From Being Dragged

**File:** `mole.css`

When you click fast, the browser may highlight an image or let you drag it. These lines turn that off.

**What to build**

Add these lines inside your `#board div img` rule. The video says to copy them from the video description.

<details>
<summary>Click to see the code</summary>

```css
    user-select: none;
    -moz-user-select: none;
    -webkit-user-drag: none;
    -webkit-user-select: none;
    -ms-user-select: none;
```

</details>

**✅ Checkpoint:** You can't highlight or drag the mole or plant anymore.

🎉 **Your game is done.** Commit and push your work to your `Games` repo on GitHub.

---

## Use Your Own Images

You can replace any of the five images with your own art from Piskel.

- **Mole and plant:** These show at 100 x 100, so make them square. Keep the background transparent so the pipe shows behind them. Animated GIFs work too.
- **Pipe, soil, and background:** Make these square as well, or use any image you like.

To use your images, either:

- name your files the same as the originals (for example, `monty-mole.png`), or
- change the file name in your code to match your file (for example, `mole.src = "./my-mole.gif";`).

---

## Troubleshooting

**Finding errors:** In the browser, press **F12** and click the **Console** tab. Errors show up in red with the file name and line number.

| Problem | Likely cause and fix |
|---|---|
| Nothing happens at all | Check the Console for errors. Check that the `<script>` tag says `mole.js` and the file is really named `mole.js`. |
| `Cannot read properties of null` | JavaScript couldn't find an element. Check the spelling of `board` and `score`, and check that you used `window.onload`. |
| The video captions say `window.unload` | It's `window.onload`. `onunload` runs when you *leave* the page, so your game would never start. |
| `... is not defined` | A function or variable name is misspelled or has the wrong capital letters. It has to match everywhere. |
| A background image doesn't show | Check the file name in `url("./...")`, including `.jpg` vs `.png`. The image must be in the same folder as your code. |
| The tiles are in one column | `display: flex;` or `flex-wrap: wrap;` is missing from `#board`. |
| The tiles spill out of the board | Check that the board is 540 x 540 and each tile is 180 x 180. |
| The mole never appears | Check the `setInterval(setMole, 1000);` line and the spelling of `monty-mole.png`. |
| Moles pile up in many pipes | The `innerHTML = "";` line is missing from the start of `setMole`. |
| Clicking the mole does nothing | The `addEventListener` line is missing from the loop, or `selectTile` is misspelled. |
| The score doesn't change | Check that the `<h2>` has `id="score"` and the code says `getElementById("score")`. |
| My change doesn't show up | Save the file (**Ctrl+S**) and refresh the browser (**F5**). |

Still stuck? Compare your code with the "Stuck?" section for that part, then ask a classmate, then ask Mr. McMaster.

---

## Try This Next

Once your game works, try some changes. Save and refresh after each one to see what happens.

1. **Change the speed.** Make the mole or plant faster or slower by changing the numbers in `setInterval`.
2. **Change the points.** Make each mole worth more or fewer points.
3. **Add a time limit.** Make the game end after 60 seconds. (Hint: look up `setTimeout`.)
4. **Add a second plant.** Make another plant that pops up in a different tile, so it's easier to lose.
5. **Make a bigger board.** Change the game to 4 x 4. You'll need to change the loop, the random number, and the tile size in the CSS.
6. **Add a Play Again button.** When the game is over, show a button that resets the score and starts again.

---

## Key Terms

| Term | Meaning |
|---|---|
| **Variable** | A named place to store a value, like `score` |
| **Function** | A named set of steps you can run, like `setMole` |
| **Loop** | Code that repeats. The `for` loop in `setGame` runs 9 times. |
| **if statement** | Code that only runs when something is true |
| **Element** | A piece of the web page, like a `div`, `img`, or `h2` |
| **id** | A name you give an element so JavaScript can find it |
| **Event** | Something that happens on the page, like a click |
| **Event listener** | Code that waits for an event and runs a function when it happens |
| **setInterval** | Runs a function over and over, every so many milliseconds |
| **Math.random** | Makes a random decimal from 0 up to 1 |
| **return** | Ends a function early |
| **this** | Inside `selectTile`, the tile that was clicked |
