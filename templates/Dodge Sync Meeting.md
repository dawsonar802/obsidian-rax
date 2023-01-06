<%*
let today = tp.date.now("YYYY-MM-DD")
let day = moment(tp.date.now("YYYY-MM-DD")).format('dddd')
let title = tp.file.title
fileName = today + " - " + day + " " + "Sync"
await tp.file.move("/Dodge/Meetings/" + tp.date.now("YYYY") + "/" + tp.date.now("MM") + "-" + tp.date.now("MMMM") + "/" + tp.file.title)
await tp.file.rename(fileName)
-%>
---
type: meeting
created: <% tp.file.creation_date() %>
date: <% tp.date.now("YYYY-MM-DD")  %>
tags: Dodge/Meeting/Sync
     todo/meetings/dodge_sync
---

### Description
A collection of notes from our weekly sync meetings.


#### Prep (Internal)

##### Notes: 
- <% tp.file.cursor() %>


#### External Notes

##### Notes: 
- 

##### Tasks
- [ ] 

###### Resources

##### Projects:
```dataview
TABLE
WITHOUT ID file.link AS "Sub Project",
status as "Status",
project as "Project"
from "Dodge/Sub-Projects"
sort status
```