<%*
// Variablen anlegen, definieren

// Art der Notiz definieren
const languageTypeOptions = [
	"HTML",
	"CSS",
	"JavaScript",
	"Java",
	"Pyton",
	"PHP",
	"C#",
	"C & C++",
	"Swift",
	"Ruby",
	"GO",
	"Rust",
	"Dos-Script",
	"Bash-Script",
	"Andere Programmiersprache"
	];
languageType = await tp.system.suggester(languageTypeOptions , languageTypeOptions);
// Artspezifische Informationen definieren
if (languageType === "Andere Programmiersprache") {
	languageOther = await tp.system.prompt("Bitte gib den Namen der Programmiersprache ein");
	if (languageOther === "" ){languageOther = noInfo};
	languageType = languageOther;
};
// Informationen definieren
autorName = await tp.system.prompt("Trage den Autor ein");
if (autorName === "" ){autorName = noInfo};
versionNr = await tp.system.prompt("Trage die Versionsnummer ein");
if (versionNr === "" ){versionNr = noInfo};
source = await tp.system.prompt("Trage die Quelle Ein. Als interner [Link] oder externer [Linkbeschreibung](URL) ein");
if (source === "" ){source = noInfo};
codeTopic = await tp.system.prompt("Beschreibe die Funktion des Codes in ein bis drei Sätzen");
if (codeTopic === "" ){codeTopic = noInfo};
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Programmiersprache:** |${languageType}|
|**Ersteller:** |${autorName}|
|**Versions Nummer** |${versionNr}|
|**Quelle:** |${source}|
|**Wichtiges über den Code:** |${codeTopic}|

## :TiSourceCode: Quellcode
\`\`\`${languageType}
// an dieser Stelle folg der ${languageType} Code.


\`\`\``;
%>

***
## :FasArrowDownShortWide: Ausführliche Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :LiBookOpenText: Beschreibung
**Zusammenfassung:**

**Wichtige Links:**

**Wissenswertes und Notizen:**

**Erweiterungen:**

**Bekannte Probleme :**

### :BoBxInfoSquare: Essenzielle Informationen
**Einsatzplattform:**

**Programmiersprache:**

**Installation:**

**Parametrisierung:**


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
[[${contentMark}${noteType}]], [[${contentMark}Development]], [[${contentMark}${languageType}]], [[${contentMark}${durability}]]`;
%>
