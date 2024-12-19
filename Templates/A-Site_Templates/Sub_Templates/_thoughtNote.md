$<%* 
// Variablen anlegen, definieren
let thoughtType, thoughtProject, thoughtOrganization, thoughtCourse, thoughtSubject, thoughtTopic, thoughtTypeOther = "";
// Artspezifische Informationen definieren
const thoughtTypeOptions = [
	"Projektgedanke",
	"Alltagsgedanken",
	"Veranstaltungsgedanke",
	"Gedanke zum Studium",
	"Idee",
	"Anderer Gedanke"
	];
thoughtType = await tp.system.suggester(thoughtTypeOptions , thoughtTypeOptions);
if (thoughtType === "Projektgedanke") {
	thoughtProject = await tp.system.prompt("Weise dem Gedanken einem Projekt zu");
	if (thoughtProject === "" ){thoughtProject = noInfo};
}
else if (thoughtType === "Gedanke zum Studium") {
	thoughtOrganization = "BFH";
	thoughtCourse = "BSc-Bachelor";
	const thoughtSubjectOptions = [
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
	thoughtSubject = await tp.system.suggester(thoughtSubjectOptions , thoughtSubjectOptions);
	if (thoughtSubject === "Anderer Fachbereich") {
		thoughtSubjectOther = await tp.system.prompt("Trage den Fachbereich ein")
		if (thoughtSubjectOther === "" ){thoughtSubjectOther = noInfo};
		thoughtSubject = thoughtSubjectOther;
	};
}
else if (thoughtType === "Anderer Gedanke") {
	thoughtTypeOther = await tp.system.prompt("Trage Art des Gedankens ein");
	if (thoughtTypeOther === "" ){thoughtTypeOther = noInfo};
	thoughtType = thoughtTypeOther;
};
const thoughtTypeSearch = ["Projektgedanke", "Alltagsgedanken", "Veranstaltungsgedanke", "Idee", thoughtTypeOther];
if (thoughtTypeSearch.includes(thoughtType)) {
	thoughtOrganization = await tp.system.prompt("Trage die durchführende Institution ein");
	if (thoughtOrganization === "" ){thoughtOrganization = noInfo};
	thoughtCourse = await tp.system.prompt("Trage die Disziplin ein");
	if (thoughtCourse === "" ){thoughtCourse = noInfo};
	thoughtSubject = await tp.system.prompt("Trage den Fachbereich ein");
	if (thoughtSubject === "" ){thoughtSubject = noInfo};
};
// Informationen definieren
thoughtTopic = await tp.system.prompt("Trage das Thema des Gedankens in ein bis zwei Sätzen ein");
if (thoughtTopic === "" ){thoughtTopic = noInfo};
// Individuelle Variablenwerte definieren
insertThoughtProject = `|**Projektname:**|${thoughtProject}| \n`;
insertThoughtOrganization = `|**Durchführende Institution:**|${thoughtOrganization}| \n`;
insertThoughtCourse = `|**Disziplin:**|${thoughtCourse}| \n`;
insertThoughtSubject = `|**Fachbereich:**|${thoughtSubject}| \n`;
// Erhobene Informationen erstellen
tR = `## :RiInformation2Line: Wichtige Informationen zum Gedanken
| | |
|:---|:---|
|**Art des Gedankes:**|${thoughtType}|\n`;
if (thoughtProject === undefined){`\n`} else if (thoughtProject === noInfo){`\n`} else {tR += insertThoughtProject};
if (thoughtOrganization === undefined){`\n`} else if (thoughtOrganization === noInfo){`\n`} else { tR += insertThoughtOrganization};
if (thoughtCourse === undefined){`\n`} else if (thoughtCourse === noInfo){`\n`} else { tR += insertThoughtCourse};
if (thoughtSubject === undefined){`\n`} else if (thoughtSubject === noInfo){`\n`} else { tR += insertThoughtSubject};
tR += `|**Thema des Gedankens:**|${thoughtTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Beschreibung des Gedankens
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :RiTaskLine: Beschreibung des Gedankens:
**Zusammenfassung:** 

**Wichtige Links:** 

**Wissenswertes und Notizen:**

**Bekannte Probleme:** 



### :BoBxInfoSquare: Essenzielle Informationen zum Gedanken:
- **Die Welt retten:** Wenn es auch noch weit weg erscheint, die Zeit rennt!



***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen zum Gedanken
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen zum Gedanken: 
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken zum Gedanken:
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen: 
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${thoughtType}]], [[${contentMark}${durability}]]`;
if (thoughtProject === undefined){}
else if (thoughtProject === noInfo){}
else { tR += `, [[${contentMark}${thoughtProject}]]` };
if (thoughtOrganization === undefined){}
else if (thoughtOrganization === noInfo){}
else {tR += `, [[${contentMark}${thoughtOrganization}]]`};
if (thoughtCourse === undefined){} 
else if (thoughtCourse === noInfo){} 
else { tR += `, [[${contentMark}${thoughtCourse}]]` };
if (thoughtSubject === undefined){}
else if (thoughtSubject === noInfo){}
else {tR += `, [[${contentMark}${thoughtSubject}]]`};
%>
