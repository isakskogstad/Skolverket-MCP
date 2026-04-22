<img width="700" height="220" alt="Skolverket MCP logo" src="https://github.com/user-attachments/assets/74563bdb-eea4-4276-a58c-ec89b11806ed" />

# Skolverket MCP Server

[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-Published-brightgreen)](https://registry.modelcontextprotocol.io/servers/io.github.isakskogstad/Skolverket-MCP)
[![MCP Protocol](https://img.shields.io/badge/MCP-2025--03--26-green)](https://modelcontextprotocol.io/)
[![License](https://img.shields.io/badge/license-MIT-orange)](LICENSE)

En [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server som ger AI-assistenter tillgång till **alla Skolverkets öppna API:er** – Läroplan API, Skolenhetsregistret och Planned Educations API. Genom att ansluta till MCP-servern kan du med hjälp av AI söka, hitta, jämföra och analysera all data och statistik som finns tillgängligt i Skolverkets öppna databaser.

---

## Snabbstart

Installera lokalt enligt guide nedan. Servern körs via stdio-transport och integreras sedan i din MCP-klient (Claude Desktop, Claude Code, Codex, Gemini, Cursor m.fl.).

### Installation från källkod

```bash
git clone https://github.com/isakskogstad/Skolverket-MCP.git
cd Skolverket-MCP
npm install
npm run build
```

Notera sökvägen till `dist/index.js` — den används i klientkonfigurationerna nedan.

<details>
<summary><strong>Klientkonfiguration</strong></summary>

<details>
<summary><strong>Claude Desktop</strong></summary>

1. I Claude Desktop: Settings → **Developer** (inte Connectors!)
2. Klicka **"Edit Config"**
3. Lägg till i JSON-filen:

```json
{
  "mcpServers": {
    "skolverket": {
      "command": "node",
      "args": ["/absolut/sökväg/till/Skolverket-MCP/dist/index.js"]
    }
  }
}
```

4. Spara och starta om Claude Desktop.

**Notera:** Lokal installation använder stdio-transport via Developer-sektionen, inte Connectors.

</details>

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude mcp add skolverket node /absolut/sökväg/till/Skolverket-MCP/dist/index.js
```

**Verifiera:** `claude mcp list`

</details>

<details>
<summary><strong>OpenAI Codex</strong></summary>

**`~/.codex/config.toml`:**

```toml
[mcp.skolverket]
command = "node"
args = ["/absolut/sökväg/till/Skolverket-MCP/dist/index.js"]
transport = "stdio"
```

**Windows:**

```toml
[mcp.skolverket]
command = "node"
args = ["C:\\Users\\username\\Skolverket-MCP\\dist\\index.js"]
transport = "stdio"
```

</details>

<details>
<summary><strong>Google Gemini / Cursor / övriga stdio-klienter</strong></summary>

Använd samma mönster — peka klienten på `node` med argumentet `/absolut/sökväg/till/Skolverket-MCP/dist/index.js` och transport `stdio`.

```json
{
  "mcpServers": {
    "skolverket": {
      "command": "node",
      "args": ["/absolut/sökväg/till/Skolverket-MCP/dist/index.js"]
    }
  }
}
```

</details>

</details>

<img width="273" height="46" alt="claudecode openaicodex googlegemini" src="https://github.com/user-attachments/assets/c4c73367-e0f5-408a-a074-83b7ce45805c" />

---

## Funktioner

Servern kopplar till tre av Skolverkets öppna API:er:

**1. Syllabus API**
Läroplaner (LGR22, GY25 m.m.), ämnen, kurser, gymnasieprogram med kunskapskrav och centralt innehåll.

**2. Skolenhetsregistret**
Sök och filtrera skolor, förskolor och andra skolenheter. Inkluderar aktiva, nedlagda och vilande enheter.

**3. Planned Educations API**
Yrkeshögskola, SFI, Komvux och andra vuxenutbildningar med startdatum, platser och studietakt.

#### Verktyg (tools)

MCP-servern implementerar MCP-protokollet med stöd för:

- **41 verktyg** – 17 Syllabus API, 4 School Units, 17 Planned Educations (inkl. gymnasieutbildningar, statistik, dokument), 3 Support Data, 1 diagnostik
- **4 resurser** – API-info, skoltyper, läroplanstyper, kurs- och ämneskoder
- **5 promptmallar** – Kursanalys, versionsjämförelser, vuxenutbildning, studievägledning, kursplanering

---

## Användningsområden

### För Lärare

- **Kursplanering:** "Jämför kunskapskraven E och A för Svenska 1 och ge förslag på bedömningsuppgifter"
- **Tematiskt arbete:** "Hitta alla kurser i gymnasiet som har hållbarhet i sitt centrala innehåll"
- **Bedömning:** "Visa alla kunskapskrav för betyg C i Biologi 1 och förklara skillnaderna mot B"

### För elever & föräldrar

- **Programval:** "Jämför Naturvetenskapsprogrammet och Teknikprogrammet - vilka kurser är obligatoriska?"
- **Kursval:** "Vilka matematikkurser finns på gymnasiet och vilka bygger på varandra?"
- **Betygskriterier:** "Vad krävs för att få A i Historia 1a1?"

### För undersökningar & analyser

- **Skolregister:** "Hitta alla aktiva gymnasieskolor i Stockholms län"
- **Kursutbud:** "Vilka skolor erbjuder Ekonomiprogrammet i Malmö?"
- **Läroplansanalys:** "Analysera hur begreppet 'programmering' har utvecklats i läroplaner 2011-2025"

https://github.com/user-attachments/assets/8eefa26c-4162-49a5-adf0-82677a663b19

---

## Övrigt

**Skapad av:** [Isak Skogstad](mailto:isak.skogstad@me.com) • [X/Twitter](https://x.com/isakskogstad)

Data från Skolverkets öppna API:er.

Villkor: Fri användning

---
