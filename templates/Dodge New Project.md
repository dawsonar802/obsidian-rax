<%*
let today = tp.date.now("YYYY-MM-DD")  
let title = tp.file.title  
if (title.startsWith("Untitled")) {  
title = await tp.system.prompt("Project Title");  
}
fileName = title  
await tp.file.move("/Dodge/Projects/" + tp.file.title)
await tp.file.rename(fileName)
const status = await tp.system.suggester(["Not Started", "In Progress", "On Hold", "Blocked", "Pending CR"], ["Not Started", "In Progress", "On Hold", "Blocked", "Pending CR"])
const title_clean = title.replace(" - ","_");
const title_clean1 = title_clean.replace(/ /g,"_");
const title_lower = title_clean1.toLowerCase()
%>
---
type: project
created: <% tp.file.creation_date() %>
date: <% tp.date.now("YYYY-MM-DD")  %>
tags: Dodge/Project
      todo/projects/<% title_lower %>
project: <% title %>
status: <% status %>
---
```button
name Update Status
type command
action MetaEdit: Run MetaEdit
```

## Description
<% tp.file.cursor() %>


##### Tasks
- [ ] 

###### Related Tasks
```dataview
TASK
WHERE project = "<% title %>" AND !completed AND text != ""
WHERE file.name != this.file.name
group by file.link
```

## 📝 Notes
- 

###### Resources
