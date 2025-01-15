<%* 
// Variablen anlegen, definieren
title = tp.file.title;
noteType = "Contentorganisation";
dateNow = tp.date.now("Do YYYY.MM.DD");
lastModifiedDate = tp.file.last_modified_date("Do YYYY.MM.DD");
substrTitle = (title.substring(5));
tag = (substrTitle.toLowerCase());
contentMark = "🌐 - ";
titleMark = ":TiWorldSearch:";
durability = "Dauerhaft";
// Alias Namen definieren
alias = await tp.system.prompt("Weise der Contentorganisation einen sprechenden Alias zu.");

// Metadaten erstellen
tR +=  `---
Erstellt am: ${dateNow}
Geändert am: ${lastModifiedDate}
aliases:
  - ${alias}
tags:
  - ${tag}/passiv
  - ${noteType}/aktiv
Notiz Typ: ${noteType}
Dauerhaftigkeit: ${durability}
---
# ${titleMark} ${noteType} - ${title}
`;
%>

##  :IbHugContentVertical: Inhaltsorganisationsliste
- Thema A, Themenzusammenfassung 
- Thema B, Themenzusammenfassung
- ...

***
## :RiAdvertisementLine: Weitere Inhaltsorganisationsinformationen 
### :LiNotepadText: Wichtige Informationen zur Inhaltsorganisation: 
%% # Hier können Informationen abgelegt werden, die in der Inhaltsorganisationsliste nicht angebracht, aber zur Anwendung der Inhaltsorganisation nützlich sind.  %%
### :SiCrowdsource: Quellen: 
%% Gibt es weitere Quellen die mit der Inhaltsorganisation in Verbindung gesetzt werden, können diese beschrieben oder verlinkt werden. %%

<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${durability}]]`;
%>
