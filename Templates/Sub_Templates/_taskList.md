<%*
// Variablen anlegen, definieren
let taskType, taskProject, taskOrganization, taskCourse, taskSubject, taskTopic, taskTypeOther = "";
// Art der Notiz definieren
const taskTypeOptions = [
	"Projekt Aufgabenliste",
	"Themenbezogene Aufgabenliste",
	"Hausaufgabenliste",
	"Allgemeine Aufgabenliste",
	"Aufgabenliste Studium",
	"Andere Aufgabenliste"
	];
taskType = await tp.system.suggester(taskTypeOptions , taskTypeOptions);
// Artspezifische Informationen definieren
if (taskType === "Projekt Aufgabenliste") {
	taskProject = await tp.system.prompt("Weise der Aufgabenliste einen Projekt zu");
	if (taskProject === "" ){taskProject = noInfo};
}
else if (taskType === "Aufgabe der BSc") {
	taskOrganization = "BFH";
	taskCourse = "BSc-Bachelor";
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
else if (taskType === "Andere Aufgabenliste") {
	taskTypeOther = await tp.system.prompt("Trage den Typ der Aufgabe ein");
	if (taskTypeOther === "" ){taskTypeOther = noInfo};
	taskType = taskTypeOther;
};
const taskTypeSearch = ["Projekt Aufgabenliste", "Themenbezogene Aufgabenliste", "Hausaufgabenliste", "Allgemeine Aufgabenliste", taskTypeOther];
if (taskTypeSearch.includes(taskType)) {
	taskOrganization = await tp.system.prompt("Trage die durchführende Institution ein");
	if (taskOrganization === "" ){taskOrganization = noInfo};
	taskCourse = await tp.system.prompt("Trage die Disziplin ein");
	if (taskCourse === "" ){taskCourse = noInfo};
	taskSubject = await tp.system.prompt("Trage den Fachbereich ein");
	if (taskSubject === "" ){taskSubject = noInfo};
};
// Informationen definieren
taskTopic = await tp.system.prompt("Trage das Thema der Aufgabenliste in ein bis zwei Sätzen ein");
if (taskTopic === "" ){taskTopic = noInfo};
// Individuelle Variablenwerte definieren
insertTaskProject = `|**Projektname:**|${taskProject}| \n`;
insertTaskOrganization = `|**Durchführende Institution:**|${taskOrganization}| \n`;
insertTaskCourse = `|**Disziplin:**|${taskCourse}| \n`;
insertTaskSubject = `|**Fachbereich:**|${taskSubject}| \n`;
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Art der Aufgabe:**|${taskType}|\n`;
if (taskProject === undefined){`\n`} else if (taskProject === noInfo){`\n`} else {tR += insertTaskProject};
if (taskOrganization === undefined){`\n`} else if (taskOrganization === noInfo){`\n`} else { tR += insertTaskOrganization};
if (taskCourse === undefined){`\n`} else if (taskCourse === noInfo){`\n`} else { tR += insertTaskCourse};
if (taskSubject === undefined){`\n`} else if (taskSubject === noInfo){`\n`} else { tR += insertTaskSubject};
tR += `|**Thema der Aufgabenliste:**|${taskTopic}|`; 
%>

***
## :FasArrowDownShortWide: Ausführliche Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :RiTaskLine: Listen Beschreibung
| Status | Thema | Aufwand in Stunden | Letztes Startdatum | Spätestes Erledigungsdatum |
|:---|:---|:---|:---|:---| 
 - [ ] Die Welt Retten, 10000, 22.11.2024, 01.01.2050
 - [ ] ... 
 
### :BoBxInfoSquare: Essenzielle Informationen
- **Die Welt retten:** Wenn es auch noch weit weg erscheint, die Zeit rennt!


***
## :RiAdvertisementLine: Weitergehende Informationen
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%

### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%

### :SiCrowdsource: Quellen
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
