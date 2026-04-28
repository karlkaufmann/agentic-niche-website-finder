# Agentic niche website finder

Experimentální **Jupyter** workflow pro objevování a hodnocení webů v úzkých (nikových) tématech pomocí **LLM agenta**, vyhledávání/SERP a **LLM-as-judge** verifikace. Repozitář je určený jako veřejná dokumentace přístupu a kódu v noteboocích — **data, výsledkové exporty ani uložené modely zde nejsou** (viz `.gitignore` a pravidla v `.cursor/rules/`).

---

## Proč tento projekt

V nikových vertikálích je důležité nejen *najít* kandidátní URL, ale i **konzistentně odhadnout**, zda jde o specializovaný obsah (blog, komunita, e-shop…) a zda stojí za zařazení do další analýzy. Notebooky modelují agentní smyčku: stahování a základní signály ze stránky, strukturované rozhodnutí auditora (LLM), metriky běhu a přehledné vizualizace.

---

## Obsah repozitáře

| Notebook | Role |
|----------|------|
| **`Agentic website finder.ipynb`** | Hlavní pipeline *Website Finder* (stav agenta, datové modely, dynamické prompty, **LLM-as-judge**, metriky, persist paměti témat v JSON). |
| **`LLM website finder.ipynb`** | Varianta zaměřená na konfiguraci a práci s LLM proxy / klientem (`LLMHandler`) nad vyhledáváním a extrakcí. |
| **`Agent Metrics.ipynb`** | **Metriky a dashboard**: načtení `agent_metrics.json`, agregace pokusů o URL, vizualizace (Plotly), export přehledu (např. HTML). |

Externí závislost v kódu: balíček `recommendation_research_llm_handler` (LLM klient). Ten musí být ve vašem prostředí nainstalovaný nebo nahrazený vlastním wrapperem kompatibilním s vaším API.

---

## Požadavky

- Python **3.10+** (doporučeno; ověřte dle vašeho stacku)
- Jupyter / VS Code / Cursor s Jupyter rozšířením
- Knihovny typicky používané v noteboocích: `pandas`, `requests`, `beautifulsoup4`, `plotly`, `openai` (dle varianty notebooku), `nest_asyncio` pro asyncio v Jupyteru
- Platné **API klíče** pro váš LLM / proxy endpoint (v notebooku často přes `getpass` — nikdy je neukládejte do repozitáře)

---

## Rychlý start

1. Vytvořte virtuální prostředí a nainstalujte závislosti podle importů v používaném notebooku (např. `pip install pandas requests beautifulsoup4 plotly nest-asyncio openai` + vlastní LLM handler).
2. Zkopírujte nebo nastavte proměnné prostředí pro váš LLM provider (např. ekvivalent k použitým klíčům v notebooku — **necommitujte** `.env` do veřejného gitu).
3. Spusťte nejdřív pipeline v **`Agentic website finder.ipynb`** nebo **`LLM website finder.ipynb`**, podle toho, kterou větev experimentu používáte.
4. Po vygenerování metrik spusťte **`Agent Metrics.ipynb`** a nasměrujte cestu k vašemu `agent_metrics.json`, pokud ji měníte.

Soubory jako `results.csv`, `agent_metrics.json` nebo `dashboard.html` jsou typicky **generované lokálně** a patří do `.gitignore`, pokud obsahují data z produkčního běhu.

---

## Metodologie (stručně)

- **Strukturované záznamy** pokusů (URL, HTTP stav, délka obsahu, heuristiky typu „ad score“) a rozhodnutí auditora (verdikt, confidence, typ webu, skóre specializace).
- **Opakovatelné měření**: agregace pokusů podle typu webu, úspěšnosti a času — vhodné pro srovnání promptů a verzí agenta.
- **Bezpečná publikace kódu**: tento remote obsahuje jen to, co je v souladu s [checklistem pro veřejný repozitář](.agent/skills/public-repo-packaging/SKILL.md) — žádné datové sady ani binární artefakty modelů.

---

## Omezení a zodpovědnost

- Výsledky závisí na kvalitě LLM, dostupnosti vyhledávání a stabilitě cílových webů.
- Notebooky mohou obsahovat **placeholdery nebo lokální cesty**; před sdílením ověřte, že v buňkách nezůstaly API klíče ani interní URL.

---

## Licence

Bez explicitní licence zůstávají práva u autora. Chcete-li repozitář forkovat, doplňte soubor `LICENSE` podle vašeho záměru.
