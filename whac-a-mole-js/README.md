# Whac-a-Mole in JavaScript

Juniors build their first JavaScript game by following a Kenny Yip Coding video. It builds on the HTML and CSS they already know. The game is made from regular HTML elements (divs and images), and JavaScript moves them around. Students write it in VS Code and run it in a web browser.

The project introduces variables, functions, if statements, loops, random numbers, timers (`setInterval`), and click events.

## Links

- **Video:** https://youtu.be/ej8SatOj3V4
- **Play the finished game:** https://imkennyyip.github.io/whac-a-mole/
- **Source code and images (teacher only):** https://github.com/ImKennyYip/whac-a-mole. This repo has the finished code, so don't share the link with students.
- **More Kenny Yip games:** https://www.kennyyipcoding.com/
- **Piskel guide** (students make their own images): [piskelGameImagesGuide.md](../piskel/piskelGameImagesGuide.md)

## Files in This Folder

| File | For | What it is |
|---|---|---|
| [whacAMoleGuide.md](whacAMoleGuide.md) | Students | The guide. Each part has steps and hints, with the code hidden in a collapsed "Stuck? Click to see the code" section. There is no complete-code section. |

## Before Class

1. **Images:** Download Kenny Yip's repo and post only these five images in Google Classroom:
   - `mario-bg.jpg`
   - `soil.png`
   - `pipe.png`
   - `monty-mole.png`
   - `piranha-plant.png`

   Don't post the code files. The guide tells students to get the images from you instead of downloading the repo, as the video says.
2. **GitHub:** Students create a new repo named `Games` and put this project in a `whac-a-mole` folder inside it. The guide's setup section walks them through it. Future games can go in the same repo, each in its own folder.
3. **How students open the guide:** The collapsed code sections stay hidden on GitHub and in VS Code's markdown preview. If students open the .md file as plain text, all the code shows.
4. **Watch the video yourself first** to make sure the pace works for your class.

## Google Classroom Post

```text
Title: Whac-a-Mole Game in JavaScript

In this project you will build your first JavaScript game, Whac-a-Mole, using HTML, CSS, and JavaScript in VS Code. Click the mole to score points, but don't click the piranha plant or the game is over.

Follow along with the video and use the attached guide (whacAMoleGuide.md) for hints and help. Try each part on your own before opening the "Stuck?" code sections. Use the images attached here. Do not download the code from GitHub.

Video: https://youtu.be/ej8SatOj3V4
Play the finished game: https://imkennyyip.github.io/whac-a-mole/

Setup: Create a new GitHub repo named Games. Inside it, make a folder named whac-a-mole for this project. Put your code files and images in that folder.

When your game works, try at least one change from the Try This Next section of the guide.

Turn in: the link to your Games repo on GitHub.
```

## Notes on the Video

The guide already handles these, but they're useful to know when helping students.

- **`window.onload`:** The video's captions say `window.unload` in one spot. The code must be `window.onload`, or the game never starts.
- **Timer speeds:** The mole starts at every 2 seconds (2000). By the end of the video, the mole is every 1 second (1000) and the plant is every 2 seconds (2000).
- **Drag-prevention CSS:** The video says to copy it from the video description. It's also in Part 12 of the guide.
- **Canvas:** The GitHub README says the game uses HTML5 canvas, but it doesn't. It uses regular HTML elements.
- **Finding errors:** Students should use the browser Console (F12) to see errors. It's the first thing in the guide's Troubleshooting section.

## After the Game

- The guide's **Try This Next** section includes the two ideas from the end of the video (a time limit and more piranha plants) plus a few more.
- Students can replace the mole, plant, and other images with their own Piskel art. The guide has a short section on it.

**Possible next games from Kenny Yip:**

- **Flappy Bird** (https://youtu.be/jj5ADM2uywg) is a step up. It uses the HTML5 canvas, a game loop, gravity, keyboard input, and collision.
  - His follow-up video on adding animations (https://youtu.be/94Vw8teCElM) is where Piskel animation frames fit in.
- **Chrome Dinosaur** (https://youtu.be/lgck-txzp9o) is about the same level as Flappy Bird.
