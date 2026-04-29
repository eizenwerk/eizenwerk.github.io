---
layout: default
title: "Best practices Logic - preferences"
---
# Best practices - Logic preferences

## Logic preferences
[https://docs.godotengine.org/en/stable/tutorials/best_practices/logic_preferences.html](https://docs.godotengine.org/en/stable/tutorials/best_practices/logic_preferences.html)

This tutorial asks the question I ask myself very often. Which kind of approach is the correct one when tackling problems? Godot has so many ways of finding solutions for programs.

#### Adding nodes and changing properties, which first?
Change values on a node before adding it to the scene tree. Sometimes that is not possible though, like with global positions.

#### load vs preloading?
Preload() loads a resource immediately when the script itself loads. It requires a static path and can only be used for constants or property defaults. It is great for dependencies you know you will need, since it front-loads the work and gives you editor autocompletion.

Load() loads a resource at the moment that line of code runs. It accepts dynamic paths but can cause hitches if it fires during performance-sensitive moments.

When to use which:
- Use preload for statble, known dependencies you will always need (like a scene or class you are "importing").
- Use load when the path might change at runtime, when you want to manage memory by loading/unloading resources on demand, or when preloading would pull in a heavy dependency chain you don't always need.

#### Large levels: static vs. dynamic
Is it better to create the level as one static space? Or is it better to load it in pieces and shift the worlds content as needed?

"When the performance requires it". Does one optimize memory or speed?

As I personally hate loading times during games, I would like to load the whole level as one static space. As I do not plan to generate massive levels, this should also not have impact on the memory or initial loading times. And tbh, people are adjusted to longer loading times, and are quite annoyed by lags or loading times during the gameplay.
The benefit of chopping it into smaller pieces is to aid in reusability of assets. A node could then manage the creation or deletion of resources in real-time, as one does not want to waste memory. This generates more complexity, which scales up the opportunities for errors and bugs.

### Project Organization
Next up, project organization
[https://docs.godotengine.org/en/stable/tutorials/best_practices/project_organization.html](https://docs.godotengine.org/en/stable/tutorials/best_practices/project_organization.html)

Godot does not force a project structure. This is godots suggestion as which workflow can be a good starting point.

#### Organization
Godot is scene based and uses the filesystem as is without metadata or an asset database. The most common approach is to group assets as close to scenes as possible.

Godot documentation example:

```gdscript
/project.godot
/docs/.gdignore  # See "Ignoring specific folders" below
/docs/learning.html
/models/town/house/house.dae
/models/town/house/window.png
/models/town/house/door.png
/characters/player/cubio.dae
/characters/player/cubio.png
/characters/enemies/goblin/goblin.dae
/characters/enemies/goblin/goblin.png
/characters/npcs/suzanne/suzanne.dae
/characters/npcs/suzanne/suzanne.png
/levels/riverdale/riverdale.scn
```

#### Style guide
- Use <mark>snake_case</mark> for folder and filenames when using gdscript for windows related issues that can popup when exporting.
- Use <mark>PascalCase</mark> for node names, as built-in nodes are also styled this way.
- Keep editor plugins and any kind of other third-party resources in the top-level addons folder.

### Version control systems
Use git or any other version control, or be mad at yourself when you loose one of your projects (or multiple) to data loss. It is also useful to backtrack changes.

Use git LFS for larger files, mainly as github has upload limitations.






Disclaimer: This post almost completely was based on the referenced godot documentation resources. I can only recommend them. This is a compact form of that documentation as this is primarly for my personal notekeeping and understanding. If you need more information, check out the official documentation.
