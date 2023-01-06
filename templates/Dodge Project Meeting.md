
<%*
folderChoicePath = "Dodge/Projects"
let filesInFolder = new Array();
filesInFolder =  app.vault.getMarkdownFiles().filter(file => file.path.includes(folderChoicePath)).map(tFile=>tFile.basename)
const project = (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles().filter(file => file.path.startsWith("Dodge/Projects")), false, "Select Related Project")).basename;
let today = tp.date.now("YYYY-MM-DD")
let title = tp.file.title
if (title.startsWith("Untitled")) {
title = await tp.system.prompt("Meeting Name");
}
fileName = today + " - " + title
await tp.file.move("/Dodge/Project Meetings/" + project+  "/" + tp.file.title)
await tp.file.rename(fileName)
const project_clean = project.replace(" - ","_");
const project_clean1 = project_clean.replace(/ /g,"_");
const project_lower = project_clean1.toLowerCase()
-%>
---
type: project_meeting
created: <% tp.file.creation_date() %>
date: <% tp.date.now("YYYY-MM-DD") %>
imageNameKey: project-<% project %>-<% tp.date.now("YYYY-MM") %>-
tags: Dodge/Meeting/Project
      todo/projects/<% project_lower %>
project: <% project %>
---

### Description
This is a meeting to discuss [[<% project %>]].
<% tp.file.cursor() %>

#### Topic

##### Tasks
- [ ] 

###### Resources
