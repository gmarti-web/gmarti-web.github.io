---
title: MTG scraper data flow diagram
permalink: /mtg-scraper-data-flow-diagram/
layout: collection
collection: mtg-scraper-dfd
date: 2025-03-19
last_modified_at: 2025-03-30
---

## Project narrative

For this project, I created a data flow diagram for an [application I built years ago](https://github.com/greg-martinez44/mtg_scraper). The application scanned tournament result pages from a Magic the Gathering netdecking website, [mtgtop8.com](https://mtgtop8.com). Then it created statistical analyses with Python in a jupyter notebook. I wrote this data flow diagram for hypothetical technical teams working on the application. I used three levels of complexity to diagram the data flow. I didn't break the flow down to the code level, as that much detail would distract from the diagram's goal.

I created these diagrams to show how to visually communicate a technical concept, such as data moving through an application. For this application, the data flow is complex. In a team setting, that flow must be understandable by anyone else. A data flow diagram lets other engineers see how data goes from the raw source to the final product. In this case, it shows data moving from the netdecking website to the statistical analyses in the jupyter notebook. Visual explanations show complex movement between programs more effectively than just words.

