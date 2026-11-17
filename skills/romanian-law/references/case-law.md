# Case law

Three layers, in this order of weight:

1. **Published Romanian decisions** in the Gazette: Constitutional Court (CCR) decisions and High Court of Cassation and Justice (ÎCCJ) decisions in the interest of the law (recurs în interesul legii) and preliminary rulings (hotărâri prealabile). Both bind: CCR decisions everyone, ÎCCJ readings all courts. Search them with the Adeveri tools.
2. **Romanian court case files**: metadata and the courts' summary solutions for cases in every court, through the court tools. They show practice, not reasoning or binding precedent. For the motivations/reasonings, you can give the dossier number for users so that they can check everything themselves at [ReJust](https://www.rejust.ro).
3. **EU case law**: CJEU judgments and orders, Advocate General opinions; see [EU law](eu-law.md).

## Published decisions

- `search` and `search_all` already note the rulings standing on a provision (`Declared unconstitutional …`, `Binding court reading … by …`): read the ruling they name.
- To find a decision, search with `act_kinds: ["decizie"]` and words of the provision or the dispute: the article and act examined (`art. 41 Codul muncii`), the competing readings or dates. `citing` the act finds every decision examining it.
- Read the decision itself, not a summary or another act quoting it.

## Reading a decision

1. Find the original decision.
2. Identify the court, the decision's number and date, the mechanism (exception of unconstitutionality, appeal in the interest of the law, preliminary ruling), and the provisions examined.
3. Read the operative part first (`DECIDE` for CCR and ÎCCJ) and classify it:
   - CCR: admitted (the provision is unconstitutional), admitted with an interpretation (constitutional only as read), rejected as unfounded, rejected as inadmissible. An inadmissible exception settles nothing about the provision's meaning.
   - ÎCCJ: the reading it fixes, and the question it answers.
4. Only then use the deciding court's reasoning.
5. Check that the decision concerns the version of the provision that applies to the facts and period.

Never attribute to the court what a party argued, what the referring court thought, the prosecutor's conclusions or a rapporteur's opinion.

## Romanian case files

The court tools search the case files of Romanian courts (when the server has them):

- Start with `search_dosare`, with an exact legal phrase, the object of the case, a party, an institution or a case number in `q`: `{ "q": "contestație la executare", "limit": 5 }`. Broaden once with a diacritic variant, one synonym or a wider procedural phrase.
- With a case number (`numar`) from the results, use `get_dosar` for parties, hearings and appeals, and `get_dosar_solutii` for the solutions over time, when the full record or the procedural history matters.
- Use `get_dosare_parte` only when the question is about a named party, with a `parte_hash` from `get_dosar`; matching names do not prove the same person or company.
- Treat `stats_solutii` as rough aggregate context, never as a prediction.
- Leave the institution, category and stage filters unset until results show the values they accept.

These results give metadata and `solutie_sumar`, not the court's reasoning. Quote the exact summary used, with the court, the case number and the dates, so the reader can find the file. A search that finds nothing does not prove that no relevant case exists; if the tools are not available or fail, say that the case-file search could not be run.

## Presenting case law

Keep apart the statute, published binding or persuasive decisions, and ordinary case results, and say which is which. Add case law to the answer when it changes or settles the practical answer; when none was found, mention it only if the user asked about case law.

Cite a published decision like any passage, `[Decizia CCR 265/2014 [3]](link)`; a case file by the fields the tools return: `<institutie>, dosar nr. <numar>, soluția din <data_pronuntare>`, with the quoted `solutie_sumar`.
