<%*
folderChoicePath = "Dodge/Projects"
let filesInFolder = new Array();
filesInFolder =  app.vault.getMarkdownFiles().filter(file => file.path.includes(folderChoicePath)).map(tFile=>tFile.basename)
const project = (await tp.system.suggester((item) => item.basename, app.vault.getMarkdownFiles().filter(file => file.path.startsWith("Dodge/Projects")), false, "Select Related Project")).basename;
let today = tp.date.now("YYYY-MM-DD")  
let title = tp.file.title  
if (title.startsWith("Untitled")) {  
title = await tp.system.prompt("Sub-Project Title");  
}
fileName = title  
await tp.file.move("/Dodge/Sub-Projects/" + project + "/" + tp.file.title)
await tp.file.rename(fileName)
const status = await tp.system.suggester(["Not Started", "In Progress", "On Hold", "Blocked", "Pending CR"], ["Not Started", "In Progress", "On Hold", "Blocked", "Pending CR"])
const project_clean = project.replace(" - ","_");
const project_clean1 = project_clean.replace(/ /g,"_");
const project_lower = project_clean1.toLowerCase()
%>
---
type: sub-project
created: <% tp.file.creation_date() %>
date: <% tp.date.now("YYYY-MM-DD") %>
tags: Dodge/Project/Sub
      todo/projects/<% project_lower %>
project: <% project %>
status: <% status %>
---
```button
name Update Status
type command
action MetaEdit: Run MetaEdit
```

### Description
This is a sub-project that is part of [[<% project %>]] . 
<% tp.file.cursor() %>

#### Topic


##### Tasks
- [ ] 


###### Status Notes


###### Resources
