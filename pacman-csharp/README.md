# Pac-Man in C# (Windows Forms)

Students build a Pac-Man game in C# with Visual Studio by following a MOO ICT video. The project introduces events, a game loop, screen coordinates, collision detection, lists and loops, and a simple class (the ghosts).

## Links

- **Video:** https://www.youtube.com/watch?v=zM8xPtzI8z0
- **Game images:** MOO ICT Patreon post "Pac Man Tutorial Game Assets" (needs a free Patreon account), file `pacman_v2_mooict_images.zip`: https://www.patreon.com/posts/pac-man-tutorial-119217850
- **Original images instead:** the [example sprite set](../piskel/exampleSprites) uses the same file names and works without changing any code
- **Piskel guide** (students make their own characters): [piskelGameImagesGuide.md](../piskel/piskelGameImagesGuide.md)

## Files in This Folder

| File | For | What it is |
|---|---|---|
| [pacmanCSharpGuide_noFullCode.md](pacmanCSharpGuide_noFullCode.md) | Students | The main guide. Code for each part, no complete-code section at the end. |
| [pacmanCSharpGuide_noFullCode_UK.md](pacmanCSharpGuide_noFullCode_UK.md) | Students | Ukrainian version. Buttons, menus, and code stay in English. |
| [pacmanCSharpGuide_withFullCode.md](pacmanCSharpGuide_withFullCode.md) | Teacher | Answer key. Same guide plus the complete `Form1.cs` and `Ghost.cs`. |

## Before Class

1. **Visual Studio:** Already checked on the lab computers. Windows Forms App (C#) is available, and the default framework is .NET 10.0. To check another computer: **Create a new project**, search `Windows Forms`, and look for **Windows Forms App** with a C# tag. If it's missing, add the **.NET desktop development** workload in the Visual Studio Installer (**Modify**). That usually needs IT.
2. **Images:** Download the images zip from Patreon once and post it in Google Classroom, so students don't need Patreon accounts. Or post the example sprite set instead.
3. **Build it yourself once** using the guide. You'll run into the same problems the students will.
4. **Time:** Plan on about two lab periods for most students, more for some.

## Google Classroom Post

```text
Title: Pac-Man Game in C#

In this project you will build a Pac-Man game in C# using Visual Studio. Follow along with the video and use the attached guide (pacmanCSharpGuide_noFullCode.md) to check your code and read what each part does.

Video: https://www.youtube.com/watch?v=zM8xPtzI8z0

Work through the guide one part at a time. At each Checkpoint, run your game and make sure it works before you move on. If you get stuck, check the Troubleshooting section in the guide, then ask a classmate, then ask Mr. McMaster.

When your game is finished, try at least two changes from the Try This Next section.

Turn in: a screenshot of your finished game and your Form1.cs and Ghost.cs files.
```

## Notes on the Video

The guide already handles these, but they're useful to know when helping students.

- **Screen wrap:** The video's wrap-around code mixes `Size` and `ClientSize`, which can make Pac-Man jump back and forth at an edge. The guide uses `ClientSize` everywhere.
- **Numbers that depend on the student's form:** The ghosts' boundary numbers and Pac-Man's starting position depend on each student's maze. The guide shows how to measure them.
- **Importing images:** Students must choose **Project resource file**, not **Local resource**. Otherwise `Properties.Resources.left` and the other image names won't work. The video doesn't point this out.
- **Framework:** The video uses .NET 8. .NET 10 works the same way.
- **Tag check:** The video uses `x.Tag == "wall"`. The guide uses `(string)x.Tag == "wall"`, which is the correct way to compare text. Both work.
- **Parameter explanation:** The narrator says passing `pacman` into a method "won't affect" the real Pac-Man. It's actually the same object. The guide explains it correctly.
- **Not in the video:** If the arrow keys don't respond, set the form's `KeyPreview` to True. If ghosts appear behind the coins, add `image.BringToFront();` in the Ghost constructor. Both are in the guide's Troubleshooting table.

## After the Game

- Require two or three changes from the guide's **Try This Next** section. Adding walls with no code changes, or adding a fifth ghost in a couple of lines, shows students why the tags and the class are useful.
- Students can replace the characters with their own Piskel art. See the [Piskel guide](../piskel/piskelGameImagesGuide.md).
