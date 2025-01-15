<%* 
// Variablen anlegen, definieren
title = tp.file.title;
dateNow = tp.date.now("DD.MM.YYYY");
lastModifiedDate = tp.file.last_modified_date("DD.MM.YYYY");
insertNoteTitle = "Sprechender Titel eingeben";
insertNoteAlias = "Sprechender Alias Titel eingeben";
noInfo = "Keine Angabe";
contentMark = "🌐 - ";

// Auswahlmenü der Notiz definieren
const noteTypeOptions =[
	"Gedankennotiz",
	"Aufgaben",
	"Deklamation",
	"Sitzungsprotokoll",
	"Medien",
	"Person",
	"Zusammenstellung",
	"Programmcode",
	"Produkt"
	];
noteType = await tp.system.suggester(noteTypeOptions , noteTypeOptions);
// Titelzuweisung, Tags und Templatezuweisung
if (noteType === "Gedankennotiz") {
	mark = "💭 ~ ";
	tag = "thought/aktiv";
	mainContent0 = "[[_thoughtNote]]";
	titleMark = ":BoBxMessageSquareDots:";
	}
else if (noteType === "Aufgaben") {
	const noteTypeOptions1 =[
		"Aufgabe",
		"Aufgabenliste"
		];
	noteType = await tp.system.suggester(noteTypeOptions1 , noteTypeOptions1);
	if (noteType === "Aufgabe") {
		mark = "🔧 ~ ";
		tag = "task/aktiv";
		mainContent0 = "[[_task]]";
		titleMark = ":RiTaskLine:";
		}
	else if (noteType === "Aufgabenliste") {
		mark = "🛠 ~ ";
		tag = "tasklist/aktiv";
		mainContent0 = "[[_taskList]]";
		titleMark = ":OcTasklist24:";
		};
	}
else if (noteType === "Sitzungsprotokoll") {
	mark = "📝 - ";
	tag = "meeting/aktiv";
	mainContent0 = "[[_meeting]]";
	titleMark = ":TiUsersGroup:";
	}
else if (noteType === "Deklamation") {
	mark = "🎪 - ";
	tag = "declamation/aktiv";
	mainContent0 = "[[_declamation]]";
	titleMark = ":BoBxBookReader:";
	}
else if (noteType === "Medien") {
	const noteTypeOptions1 =[
		"Internet Medien",
		"Print Medien",
		"Radio & TV Medien"
		];
	noteType = await tp.system.suggester(noteTypeOptions1 , noteTypeOptions1);
	if (noteType === "Internet Medien") {
		mark = "☁ - ";
		tag = "medium-internet/aktiv";
		mainContent0 = "[[_mediumInternet]]";
		titleMark = ":LiCloudy:";
	}
	else if (noteType === "Print Medien") {
		mark = "📙 - ";
		tag = "medium-print/aktiv";
		mainContent0 = "[[_mediumPrint]]";
		titleMark = ":BoBxsBookBookmark:";
		}
	else if (noteType === "Radio & TV Medien") {
		mark = "📺 - ";
		tag = "medium-radiotv/aktiv";
		mainContent0 = "[[_mediumRadioTV]]";
		titleMark = ":BoBxRadio:";
		};
	}
else if (noteType === "Person") {
	mark = "🕵️‍♂️ - ";
	tag = "person/aktiv";
	mainContent0 = "[[_person]]";
	titleMark = ":FasPersonChalkboard:";
	}
else if (noteType === "Zusammenstellung") {
mark = "📑 - ";
tag = "collocation/aktiv";
mainContent0 = "[[_collocation]]";
titleMark = ":CoLayers:";
	}
else if (noteType === "Programmcode") {
	mark = "💾 - ";
	tag = "sourcecode/aktiv";
	mainContent0 = "[[_sourceCode]]";
	titleMark = ":TiDeviceIpadHorizontalCode:";
	}
else if (noteType === "Produkt") {
	mark = "💎 - ";
	tag = "product/aktiv";
	mainContent0 = "[[_product]]";
	titleMark = ":TiDiamond:";
};

//Titel generieren
if (title.startsWith("Untitled")) { 
	title = await tp.system.prompt(insertNoteTitle);
	await tp.file.rename(mark + title);
	};
//Beständigkeit festlegen anhand "mark" Variablen
if (mark.endsWith("- ")) { 
	durability = "Dauerhaft";
	}
else if (mark.endsWith("~ ")) {
	durability = "Befristet";
	}
else {
	durability = "Unbekannt";
};

// Aliasnamen definieren
alias = await tp.system.prompt(insertNoteAlias);
// Metadaten erstellen
tR +=  `---
Erstellt am: ${dateNow}
Geändert am: ${lastModifiedDate}
aliases:
  - ${alias}
tags:
  - ${tag}
Notiz Typ: ${noteType}
Dauerhaftigkeit: ${durability}
---
# ${titleMark} ${noteType} - ${title}

`; 
%>
<% tp.file.include(mainContent0) %>