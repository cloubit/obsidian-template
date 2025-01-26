<%*
// Variablen anlegen, definieren
let insertProjectName;
// Art der Notiz definieren
const meetingTypeOptions = [
	"Projektsitzung",
	"Teamsitzung",
	"Themensitzung",
	"Krisensitzung",
	"Andere"
	];
meetingType = await tp.system.suggester(meetingTypeOptions , meetingTypeOptions);
// Artspezifische Informationen definieren
if (meetingType === "Projektsitzung") {
	projectName = await tp.system.prompt("Trage den Projektnamen ein");
	insertProjectName = `|**Projektname:**|${projectName}| \n`;
}
else if (meetingType === "Andere") {
	meetingOther = await tp.system.prompt("Trage den Sitzungstyp ein");
	if (meetingOther === "" ){meetingOther = noInfo};
	meetingType = meetingOther;
};
// Informationen definieren
meetingTopic = await tp.system.prompt("Trage das Thema der Sitzung ein");
if (meetingTopic === "" ){meetingTopic = noInfo};
meetingDate = await tp.system.prompt("Trage das Sitzungsdatum ein");
if (meetingDate === "" ){meetingDate = noInfo};
meetingTime = await tp.system.prompt("Trage die Zeit der Sitzung ein");
if (meetingTime === "" ){meetingTime = noInfo};
meetingOrganiser = await tp.system.prompt("Trage den Sitzungsorganisator ein");
if (meetingOrganiser === "" ){meetingOrganiser = noInfo};
const meetingStatusOptions = [
	"Sitzung geplant",
	"Sitzung durchgeführt"
	];
meetingStatus = await tp.system.suggester(meetingStatusOptions, meetingStatusOptions);
if (meetingStatus === "Sitzung geplant") {
	meetingStatus = "geplant";
	} else {
	meetingStatus = "durchgeführt";
};
venue = await tp.system.prompt("Trage den Sitzungsort ein");
if (venue === "" ){venue = noInfo};
participants = await tp.system.prompt("Trage die Sitzungsteilnehmenden ein");
if (participants === "" ){participants = noInfo};
// Erhobene Informationen erstellen
tR +=  `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Sitzungstyp:**|${meetingType}| \n`;
if (insertProjectName === undefined){`\n`} else { tR += insertProjectName};
tR += `|**Thema der Sitzung:**|${meetingTopic}|
|**Datum der Sitzung:**|${meetingDate}|
|**Durchführungszeit der Sitzung:**|${meetingTime}|
|**Sitzungsverantwortlicher**|${meetingOrganiser}|
|**Status der Sitzung**|${meetingStatus}|
|**Ort der Sitzung:**|${venue}|
|**Teilnehmende:**|${participants}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :OcProjectRoadmap24: Agenda, Schwerpunkte und Beschreibung
 1. Begrüssung
 2. Vorstellung der Teilnehmenden
 3. ...

### :LiBookOpenText: Wichtige Beschlüsse
<%*
// Beschlusstabelle mit Protokollverantwortlichkeit erstellen
tR+= `| Thema | Beschluss | Verantwortlichkeit | Erledigt bis |
|:--- |:---|:---|:---|
| Sitzungsprotokoll | Fertigstellung und Versand an Teilnehmende | ${meetingOrganiser} | ${dateNow} |
| | | |
| | | |`;
%>

### :RaSpeechBubbles: Themenbezogene Diskusionspunkte
- **Erster Diskusionspunkt:**
- **Zweiter Diskusionspunkt:**

### :FasShoePrints: Nächste Schritte


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen:
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%

### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%

### :SiCrowdsource: Quellen
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links
[[${contentMark}${noteType}]], [[${contentMark}${meetingType}]], [[${contentMark}${durability}]]`;
if (insertProjectName === undefined){}
else if (projectName === noInfo){}
else { tR += `, [[${contentMark}${projectName}]]` };
%>
