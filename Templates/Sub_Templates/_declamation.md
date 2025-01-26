<%*
// Variablen anlegen, definieren
let lectureType, lectureProject, lectureOrganization, lectureCourse, lectureSubject, lectureDate, lecturer, lectureLocation, lectureTopic, lectureTypeOther = "";
// Art der Notiz definieren
const lectureTypeOptions = [
	"Projekt Deklamation",
	"Einfacher-Vortrag",
	"Einfache-Vorlesung",
	"Vorlesung Studium",
	"Andere Deklamation"
	];
lectureType = await tp.system.suggester(lectureTypeOptions , lectureTypeOptions);
// Artspezifische Informationen definieren
if (lectureType === "Projekt Deklamation") {
	lectureProject = await tp.system.prompt("Weise der Deklamation einem Projekt zu");
	if (lectureProject === "" ){lectureProject = noInfo};
}
else if (lectureType === "Vorlesung Studium") {
	lectureOrganization = "BFH";
	lectureCourse = "BSc-Bachelor";
	const lectureSubjectOptions = [
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
	lectureSubject = await tp.system.suggester(lectureSubjectOptions , lectureSubjectOptions);
	if (lectureSubject === "Anderer Fachbereich") {
		lectureSubjectOther = await tp.system.prompt("Trage die Fachbereich ein")
		if (lectureSubjectOther === "" ){lectureSubjectOther = noInfo};
		lectureSubject = lectureSubjectOther;
	};
}
else if (lectureType === "Andere Deklamation") {
	lectureTypeOther = await tp.system.prompt("Trage den Typ der Deklamation ein");
	if (lectureTypeOther === "" ){lectureTypeOther = noInfo};
	lectureType = lectureTypeOther;
};
const lectureTypeSearch = ["Projekt Deklamation", "Einfacher Vortrag", "Einfache Vorlesung", lectureTypeOther];
if (lectureTypeSearch.includes(lectureType)) {
	lectureOrganization = await tp.system.prompt("Trage die durchführende Institution ein");
	if (lectureOrganization === "" ){lectureOrganization = noInfo};
	lectureCourse = await tp.system.prompt("Trage die Disziplin ein");
	if (lectureCourse === "" ){lectureCourse = noInfo};
	lectureSubject = await tp.system.prompt("Trage den Fachbereich ein");
	if (lectureSubject === "" ){lectureSubject = noInfo};
};
// Informationen definieren
lectureTopic = await tp.system.prompt("Trage das Thema der Deklamation in ein bis zwei Sätzen ein");
if (lectureTopic === "" ){lectureTopic = noInfo};
lectureDate = await tp.system.prompt("Trage das Datum der Deklamation ein");
if (lectureDate === "" ){lectureDate = noInfo};
lecturer = await tp.system.prompt("Trage den Dozent ein, der die Deklamation durchführt");
if (lecturer === "" ){lecturer = noInfo};
lectureLocation = await tp.system.prompt("Trage den Durchführungsort der Deklamation ein");
if (lectureLocation === "" ){lectureLocation = noInfo};
// Individuelle Variablenwerte definieren
insertLectureProject = `|**Projektname:**|${lectureProject}| \n`;
insertLectureOrganization = `|**Durchführende Institution:**|${lectureOrganization}| \n`;
insertLectureCourse = `|**Disziplin:**|${lectureCourse}| \n`;
insertLectureSubject = `|**Fachbereich:**|${lectureSubject}| \n`;
insertLectureDate = `|**Datum :**|${lectureDate}| \n`;
insertLecturer = `|**Dozent:**|${lecturer}| \n`;
insertLectureLocation = `|**Ort der Durchführung:**|${lectureLocation}| \n`;
// Erhobene Informationen erstellen
tR +=  `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Art der Notiz:**|${lectureType}|\n`;
if (lectureProject === undefined){`\n`} else if (lectureProject === noInfo){`\n`} else {tR += insertLectureProject};
if (lectureOrganization === undefined){`\n`} else if (lectureOrganization === noInfo){`\n`} else { tR += insertLectureOrganization};
if (lectureCourse === undefined){`\n`} else if (lectureCourse === noInfo){`\n`} else { tR += insertLectureCourse};
if (lectureSubject === undefined){`\n`} else if (lectureSubject === noInfo){`\n`} else { tR += insertLectureSubject};
if (lectureDate === undefined){`\n`} else if (lectureDate === noInfo){`\n`} else { tR += insertLectureDate};
if (lecturer === undefined){`\n`} else if (lecturer === noInfo){`\n`} else { tR += insertLecturer};
if (lectureLocation === undefined){`\n`} else if (lectureLocation === noInfo){`\n`} else { tR += insertLectureLocation};
tR += `|**Thema der Notiz:**|${lectureTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :OcProjectRoadmap24: Schwerpunkte und Beschreibung
 1. **Begrüssung**
 2. .
 3. ...

### :LiBookOpenText: Essentielle Notizen

### :RaSpeechBubbles: Themenbezogene Diskusionspunkte
- **Erster Diskusionspunkt:**
- **Zweiter Diskusionspunkt:**

### :FasShoePrints: Offene Fragen und Nachforschung


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
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
tR += `### :CoLink: Weitere interne Links
[[${contentMark}${noteType}]], [[${contentMark}${lectureType}]], [[${contentMark}${durability}]]`;
if (lectureProject === undefined){}
else if (lectureProject === noInfo){}
else { tR += `, [[${contentMark}${lectureProject}]]` };
if (lectureOrganization === undefined){}
else if (lectureOrganization === noInfo){}
else {tR += `, [[${contentMark}${lectureOrganization}]]`};
if (lectureCourse === undefined){}
else if (lectureCourse === noInfo){}
else {tR += `, [[${contentMark}${lectureCourse}]]`};
if (lectureSubject === undefined){}
else if (lectureSubject === noInfo){}
else {tR += `, [[${contentMark}${lectureSubject}]]`};
%>
