# rulespec-bo Agent Notes

This repo stores Bolivia RuleSpec source registry materials, oracle references, and encoded policy rules. All encoded law lives under a single `bo/` namespace.

## Scope

- `bo/statutes/`: Bolivian laws - Ley 843 (texto ordenado DS 27947 Anexo 3), Ley 065 de 2010 (pensiones), Ley 3791 de 2007 (Renta Dignidad), and other primary law needed for tax-benefit modeling.
- `bo/regulations/`: decretos supremos and institutional resolutions (DS 28899 Juancito Pinto, DS 0066 Juana Azurduy, DS 21531 RC-IVA reglamento, COVID-19 bono decrees) made under the laws.
- `bo/policies/`: social-protection programme rules set administratively (reglamentos operativos de los bonos).
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/coverage/`, `data/oracles/`: coverage backlog and comparison references. These are never legal authority.

## Do

- Start from the furthest upstream source: Gaceta Oficial texts first, state-institution prints (BCB, APS, ministry files) next, agency guidance last - record the host in manifest metadata.
- Respect the capture hazards (see README): the gazette PDF endpoint OOMs server-side (use the verGratis_gob HTML norm view); the SIN Compendio print carries a reproduction prohibition (never capture it); www.bja.gob.bo serves an expired certificate (manifest `local_path` with recorded source_url + sha256; never disable verification).
- Add RuleSpec under `bo/statutes/`, `bo/regulations/`, or `bo/policies/` with companion `.test.yaml` files.
- Cite corpus paths from modules via `module.source_verification.corpus_citation_path` (or `corpus_citation_paths`).
- Use the BOLMOD v2.1 policy window (2019-23) as the validation frame: RC-IVA 13%; VAT 13%; SIP 10% + 1.71% + 0.5% + 0.5% (er 3%); national solidarity 1/5/10% over Bs13k/25k/35k; Renta Dignidad Bs3,900/4,550; Juancito Pinto Bs200. Indexed/annual values must be corpus-grounded, never invented.
- Keep exact oracle versions in `data/oracles/oracle-index.json`. The SOUTHMOD bundle is licensed and non-redistributable - never commit bundle bytes, dataset rows, or model XML.
- Sync `axiom-encode` and `.axiom/toolchain.toml` before substantial encoding runs.

## Do Not

- Use SIN calculators or third-party tax alerts as the first legal source when a law or instrument governs the rule.
- Invent, round, or interpolate any Bolivian monetary amount, rate band, or threshold. Every number must come verbatim from a captured official provision.
- Migrate BOLMOD, EUROMOD/SOUTHMOD, or agency calculator code mechanically as RuleSpec.
- Add generated source payload dumps, formula artifacts, `parameters.yaml`, or standalone YAML fixtures outside allowed RuleSpec roots.
- Hand-copy statute text into RuleSpec without a corpus `citation_path`.
