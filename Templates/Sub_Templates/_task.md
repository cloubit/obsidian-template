<%*
// Variablen anlegen, definieren
let taskType, taskProject, taskOrganization, taskCourse, taskSubject, taskTopic, taskTypeOther = "";
// Art der Notiz definieren
const taskTypeOptions = [
	"Projekt Aufgabe",
	"Themenbezogene Aufgabe",
	"Hausaufgabe",
	"Allgemeine Aufgabe",
	"Aufgabe Studium",
	"Andere Aufgabe"
	];
taskType = await tp.system.suggester(taskTypeOptions , taskTypeOptions);
// Artspezifische Informationen definieren
if (taskType === "Projekt Aufgabe") {
	taskProject = await tp.system.prompt("Weise die Aufgabe einen Projekt zu");
	if (taskProject === "" ){taskProject = noInfo};
}
else if (taskType === "Aufgabe Studium") {
	// Durchführende Organisation wird definiert
	taskOrganization = "BFH";
	// Disziplin definieren
	taskCourse = "BSc-Bachelor";
	// Fachbereich definieren
	const taskSubjectOptions = [
	"Professionelle Pflege",
	"Klinisches Assessment",
	"Technical English",
	"Discreptive Statistik",
	"Inferenzstatistik",
	"Gesundheitsökonomie und Gesundheitsstatistik",
	"Beratung und eHealth",
	"Basiswissen Forschung",
	"Systemische Pflege und Ethik",
	"Anderer Fachbereich"
	];
	taskSubject = await tp.system.suggester(taskSubjectOptions , taskSubjectOptions);
	if (taskSubject === "Anderer Fachbereich") {
		taskSubjectOther = await tp.system.prompt("Trage den Fachbereich ein")
		if (taskSubjectOther === "" ){taskSubjectOther = noInfo};
		taskSubject = taskSubjectOther;
	};
}
else if (taskType === "Andere Aufgabe") {
	taskTypeOther = await tp.system.prompt("Trage Art der Aufgabe ein");
	if (taskTypeOther === "" ){taskTypeOther = noInfo};
	taskType = taskTypeOther;
};
const taskTypeSearch = ["Projekt Aufgabe", "Themenbezogene Aufgabe", "Hausaufgabe", "Allgemeine Aufgabe", taskTypeOther];
if (taskTypeSearch.includes(taskType)) {
	taskOrganization = await tp.system.prompt("Trage die durchführende Institution ein");
	if (taskOrganization === "" ){taskOrganization = noInfo};
	taskCourse = await tp.system.prompt("Trage die Disziplin ein");
	if (taskCourse === "" ){taskCourse = noInfo};
	taskSubject = await tp.system.prompt("Trage den Fachbereich ein");
	if (taskSubject === "" ){taskSubject = noInfo};
};
// Informationen definieren
taskTopic = await tp.system.prompt("Trage das Thema der Aufgabe ein");
if (taskTopic === "" ){taskTopic = noInfo};
taskRealisationTime = await tp.system.prompt("Trage den geplanten Aufwand zur Erledigung der Aufgabe ein");
if (taskRealisationTime === "" ){taskRealisationTime = noInfo};
taskLatestStartDate = await tp.system.prompt("Trage das Startdatum der Aufgabe im Format DD.MM.YYYY ein. Wird kein Wert angegeben wird das Datum von Morgen eingetragen");
if (taskLatestStartDate === "" ){taskLatestStartDate = tp.date.now("DD.MM.YYYY", 1)};
taskEndDate = await tp.system.prompt("Trage den spätester Erledigungstermin im Format DD.MM.YYYY ein. Wird kein Wert eingetragen wird das Datum heute in zwei Wochen eingetragen");
if (taskEndDate === "" ){taskEndDate = tp.date.now("DD.MM.YYYY", 14)};
// Individuelle Variablenwerte definieren
insertTaskProject = `|**Projektname:**|${taskProject}| \n`;
insertTaskOrganization = `|**Durchführende Institution:**|${taskOrganization}| \n`;
insertTaskCourse = `|**Disziplin:**|${taskCourse}| \n`;
insertTaskSubject = `|**Fachbereich:**|${taskSubject}| \n`;
insertTaskRealisationTime = `|**Geplanter Aufwand in Stunden:**|${taskRealisationTime}| \n`;
insertTaskLatestStartDate = `|**Letztes Start Datum **|${taskLatestStartDate}| \n`;
insertTaskEndDate = `|**Spätestes Erledigungsdatum:**|${taskEndDate}| \n`;
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Wichtige Aufgabeninformationen
| | |
|:---|:---|
|**Art der Aufgabe:**|${taskType}|\n`;
if (taskProject === undefined){`\n`} else if (taskProject === noInfo){`\n`} else {tR += insertTaskProject};
if (taskOrganization === undefined){`\n`} else if (taskOrganization === noInfo){`\n`} else { tR += insertTaskOrganization};
if (taskCourse === undefined){`\n`} else if (taskCourse === noInfo){`\n`} else { tR += insertTaskCourse};
if (taskSubject === undefined){`\n`} else if (taskSubject === noInfo){`\n`} else { tR += insertTaskSubject};
if (taskRealisationTime === undefined){`\n`} else if (taskRealisationTime === noInfo){`\n`} else { tR += insertTaskRealisationTime};
if (taskLatestStartDate === undefined){`\n`} else if (taskLatestStartDate === noInfo){`\n`} else { tR += insertTaskLatestStartDate};
if (taskEndDate === undefined){`\n`} else if (taskEndDate === noInfo){`\n`} else { tR += insertTaskEndDate};
tR += `|**Thema der Aufgabe:**|${taskTopic}|`; 
%>

***
## :FasArrowDownShortWide: Ausführliche Beschreibung der Aufgabe
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :OcProjectRoadmap24: Aufgabenbeschreibung:
**Zusammenfassung:**

**Wissenswertes und Notizen:**

**Mögliche Varianten:**


### :BoBxInfoSquare: Essenzielle Informationen zur Aufgabenerledigung:
**Vorgaben:**


### :RaSpeechBubbles: Unstrukturierte Gedanken zur Aufgabe:
**Umsetzungsideen:**


### :FasShoePrints: Prozessschritte zur Erledigung der Aufgabe:
1. Informationen Sammeln
2. Informationen Sortieren
3. Informationen Auswerten
4. ... 


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen zur Aufgabe
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen zur Aufgabe: 
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken zur Aufgabe:
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen: 
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${taskType}]], [[${contentMark}${durability}]]`;
if (taskProject === undefined){}
else if (taskProject === noInfo){}
else { tR += `, [[${contentMark}${taskProject}]]` };
if (taskOrganization === undefined){}
else if (taskOrganization === noInfo){}
else {tR += `, [[${contentMark}${taskOrganization}]]`};
if (taskCourse === undefined){} 
else if (taskCourse === noInfo){} 
else { tR += `, [[${contentMark}${taskCourse}]]` };
if (taskSubject === undefined){}
else if (taskSubject === noInfo){}
else {tR += `, [[${contentMark}${taskSubject}]]`};
%>
