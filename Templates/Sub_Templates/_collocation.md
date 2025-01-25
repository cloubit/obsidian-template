<%*
// Variablen anlegen, definieren
let collocationType, collocationProject, autorName, collocationStatus, versionNr, source, collocationTopic = "";
// Art der Notiz definieren
const collocationTypeOptions = [
	"Readme",
	"Installationsanleitung",
	"Montageanleitung",
	"Bedienungsanleitung",
	"Leitfaden",
	"Betriebshandbuch",
	"Gebrauchsanleitung",
	"Systemkonfiguration",
	"Rezept",
	"Zusammenstellung",
	"Andere Zusammenstellung"
	];
collocationType = await tp.system.suggester(collocationTypeOptions , collocationTypeOptions);
// Artspezifische Informationen definieren
if (collocationType === "Andere Zusammenstellung") {
	collocationOther = await tp.system.prompt("Bitte gib den Dokument Organisationstyp ein");
	if (collocationOther === "" ){collocationOther = noInfo};
	collocationType = collocationOther;
};
// Informationen definieren
collocationProject = await tp.system.prompt("Weise der Zusammenstellung einen Projekt zu.");	
if (collocationProject === "" ){collocationProject = noInfo};
autorName = await tp.system.prompt("Trage den Autor ein");
if (autorName === "" ){autorName = noInfo};
collocationStatus = await tp.system.prompt("Trage den Status ein");
if (collocationStatus === "" ){collocationStatus = noInfo};
versionNr = await tp.system.prompt("Trage die Versionsnummer ein");
if (versionNr === "" ){versionNr = noInfo};
source = await tp.system.prompt("Trage die Quelle Ein. Als interner [Link] oder externer [Linkbeschreibung](URL) ein");
if (source === "" ){source = noInfo};
collocationTopic = await tp.system.prompt("Beschreibe die Zusammenstellung in ein bis drei Sätzen");
if (collocationTopic === "" ){collocationTopic = noInfo};
// Individuelle Variablenwerte definieren
insertCollocationProject = `|**Projektname:**|${collocationProject}| \n`;
insertAutorName = `|**Ersteller:** |${autorName}| \n`;
insertCollocationStatus = `|**Status** |${collocationStatus}| \n`;
insertVersionNr = `|**Versions Nummer** |${versionNr}| \n`;
insertSource = `|**Quelle:** |${source}| \n`;
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Art der Notiz:** |${collocationType}| \n`;
if (collocationProject === undefined){`\n`} else if (collocationProject === noInfo){`\n`} else {tR += insertCollocationProject};
if (autorName === undefined){`\n`} else if (autorName === noInfo){`\n`} else {tR += insertAutorName};
if (collocationStatus === undefined){`\n`} else if (collocationStatus === noInfo){`\n`} else {tR += insertCollocationStatus};
if (versionNr === undefined){`\n`} else if (versionNr === noInfo){`\n`} else {tR += insertVersionNr};
if (source === undefined){`\n`} else if (source === noInfo){`\n`} else {tR += insertSource};
tR += `|**Thema der Notiz:** |${collocationTopic}|`;
%>

***
## :FasArrowDownShortWide: Wichtige Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%
##  :LiBookOpenText: Beschreibung
**Zusammenfassung:** 

**Anforderungen für die Integration oder die Entwicklungsumgebung:** 

**Anleitung zur Installation und der Bedienung:**

**Verwendete Technologien:**

**Erweiterungsmöglichkeiten:**

**bekannte Probleme :** 

**FAQ**

**Copyright und Lizenz Informationen**


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
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${collocationType}]], [[${contentMark}${durability}]],[[${contentMark}${collocationProject}]]`;
%>
