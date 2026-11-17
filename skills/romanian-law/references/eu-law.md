# EU law

The Adeveri server holds Romanian law only. Search EU legislation and CJEU case law at the EU Publications Office (Cellar), which answers plain HTTP GET requests, and cite EUR-Lex. EUR-Lex pages themselves refuse automated requests (an empty `202` answer): link to them, do not fetch them.

## How to search

- Query in Romanian first when the user writes in Romanian: EU acts have official Romanian titles and texts. Use English only as a fallback, after Romanian finds nothing usable, and say so.
- Search every material layer in the first batch: a sector rule (toy safety) and the horizontal rule on the same facts (general product safety, operator responsibility, withdrawal, recall, sanctions). Keep and cite every layer that governs the facts.
- Use a known CELEX, ECLI or case number directly. For the law on a past day, take the consolidated version in force then.
- Look for case law when the CJEU's reading may matter; for a direct request for a definition or rule, the legislation suffices.
- Then search the Romanian side with the Adeveri tools: for a directive, the Romanian law transposing it (`search` its number, `2009/48/CE`, with the topic); for a regulation, the Romanian authority, procedure and sanctions applying it.

## Cellar

Every query below is a SPARQL `SELECT` sent as a GET request:

```
https://publications.europa.eu/webapi/rdf/sparql?query=<URL-encoded query>&format=application/sparql-results+json
```

All use `PREFIX cdm: <http://publications.europa.eu/ontology/cdm#>`; string literals are typed `^^<http://www.w3.org/2001/XMLSchema#string>` (written `^^xsd:string` below, with `PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>`). Lookups by CELEX or ECLI answer in about a second; a search of titles can take up to a minute, so allow a long timeout and keep `LIMIT`.

CELEX numbers tell what a document is: `3` + year + `R` (regulation), `L` (directive) or `D` (decision) + number (`32023R0988`); `0` + the act's CELEX + `-` + the version's date for a consolidated version (`02011R1169-20250401`); `6` + year + `CJ` (Court judgment), `CC` (Advocate General opinion), `CO` (order) or `TJ` (General Court judgment) + the case number (`C-311/18` is `62018CJ0311`).

**Acts in force whose Romanian title contains a phrase.** Use a short phrase the title would hold, in lower case with the official diacritics (`ș`, `ț`):

```sparql
SELECT DISTINCT ?celex ?title WHERE {
  ?work cdm:resource_legal_id_celex ?celex ;
        cdm:resource_legal_in-force "true"^^xsd:boolean .
  ?expression cdm:expression_belongs_to_work ?work ;
        cdm:expression_uses_language <http://publications.europa.eu/resource/authority/language/RON> ;
        cdm:expression_title ?title .
  FILTER(STRSTARTS(?celex, "3") && CONTAINS(LCASE(?title), "siguranța generală a produselor"))
} LIMIT 10
```

Drop the `in-force` line to find repealed acts too; start the CELEX filter with `6` instead of `3` for case law by words of its title (CJEU titles list the subject matter, `Trimitere preliminară – …`).

**The consolidated versions of an act**, newest first; take the newest dated on or before the day that matters:

```sparql
SELECT ?celex WHERE {
  ?work cdm:resource_legal_id_celex ?celex .
  FILTER(STRSTARTS(?celex, "02011R1169-"))
} ORDER BY DESC(?celex) LIMIT 20
```

**The Romanian text of a document** (an act, a consolidated version, a judgment): find its XHTML manifestation, then GET that address followed by `/DOC_1`. Texts reach a few MB: save the file and search it with your own tools (`Articolul 9`, a phrase) instead of reading it whole.

```sparql
SELECT ?manifestation WHERE {
  ?work cdm:resource_legal_id_celex "02011R1169-20250401"^^xsd:string .
  ?expression cdm:expression_belongs_to_work ?work ;
        cdm:expression_uses_language <http://publications.europa.eu/resource/authority/language/RON> .
  ?manifestation cdm:manifestation_manifests_expression ?expression ;
        cdm:manifestation_type "xhtml"^^xsd:string .
}
```

A tool that can set request headers may instead GET `https://publications.europa.eu/resource/celex/<CELEX>` with `Accept: application/xhtml+xml` and `Accept-Language: ron`.

**Case law interpreting an act**, newest first:

```sparql
SELECT DISTINCT ?celex ?ecli WHERE {
  ?act cdm:resource_legal_id_celex "32004R0261"^^xsd:string .
  ?case cdm:case-law_interpretes_resource_legal ?act ;
        cdm:resource_legal_id_celex ?celex .
  OPTIONAL { ?case cdm:case-law_ecli ?ecli }
} ORDER BY DESC(?celex) LIMIT 20
```

**A ruling by its ECLI**:

```sparql
SELECT ?celex WHERE {
  ?case cdm:case-law_ecli "ECLI:EU:C:2025:139"^^xsd:string ;
        cdm:resource_legal_id_celex ?celex .
}
```

## Reading what you find

- A consolidated version is a documentation aid, not the authentic text: say which version you quote, and check the original act (and its corrigenda) when the wording is decisive.
- A recital explains; it does not oblige. Cite the article.
- Judgments decide; Advocate General opinions (`CC`) may persuade but are not the Court's holding; orders (`CO`) often only close a case. Read the operative part first, then the reasoning. A preliminary ruling interprets EU law; it does not decide the national dispute.
- A search that found nothing, or a service that did not answer, cannot support a claim that no EU rule exists: say what could not be searched.

## Citing

Link each act or ruling to EUR-Lex with its CELEX, and quote the passage relied on with its article, paragraph or point:

```
https://eur-lex.europa.eu/legal-content/RO/TXT/?uri=CELEX:<CELEX>
```

For example:

> Potrivit [Regulamentului (UE) 2023/988, art. 9 alin. (1)](https://eur-lex.europa.eu/legal-content/RO/TXT/?uri=CELEX:32023R0988), producătorii „se asigură că produsele respective au fost proiectate și fabricate în conformitate cu cerința generală de siguranță".
 Cite a consolidated version by its own CELEX (`02011R1169-20250401`), and a ruling with its ECLI.
