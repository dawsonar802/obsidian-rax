<%* 
const title = await tp.system.prompt("Note Title"); 
const folders = this.app.vault.getAllLoadedFiles().filter(i => i.children).map(folder => folder.path); 
const folderChoicePath = await tp.system.suggester(folders, folders); 
const folder = app.vault.getAbstractFileByPath(folderChoicePath); 
const template = tp.file.find_tfile("Meeting").basename 
await tp.file.create_new(template,title,true,folder).basename 
%>