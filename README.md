# rulespec-bo

Bolivia RuleSpec source registry.

This repository targets the Bolivian tax-benefit surface simulated by BOLMOD (the SOUTHMOD tax-benefit microsimulation model for Bolivia, UNU-WIDER; v2.1, policy years 2019-23): the complementary regime to VAT RC-IVA (13 percent, Ley 843 texto ordenado Art. 30) and VAT (13 percent general rate, Art. 15), the transactions tax IT and excises ICE under the same code, SIP pension contributions under Ley 065 de 2010 (retirement 10 percent; severance 1.71 percent; administration 0.5 percent; solidarity 0.5 percent employee plus 3 percent employer; national solidarity bands of 1/5/10 percent over Bs13,000/25,000/35,000 monthly), Renta Dignidad under Ley 3791 de 2007 (universal old-age income at 60+: Bs3,900 annual for pension recipients, Bs4,550 for non-recipients), and the Bono Juancito Pinto (DS 28899 de 2006; Bs200 annual per eligible pupil) and Bono Juana Azurduy (DS 0066 de 2009) conditional cash transfers.

All encoded law lives under a single `bo/` namespace. The validation frame is BOLMOD v2.1 (report CR-BOLMOD-v2-1, Tables 2.4-2.15).

## Source Priority

Policy must come from the furthest upstream available source: Gaceta Oficial texts and official consolidations first (the DS 27947 Anexo 3 texto ordenado of Ley 843 is captured from the gazette norm view - the gazette PDF endpoint fails server-side, and the SIN Compendio print is NOT capturable: it carries an explicit reproduction-prohibition watermark), state-institution prints next (BCB, APS, ministry files - record the host in manifest metadata), agency guidance only after the governing instrument is identified. www.bja.gob.bo serves an expired server certificate: fetch out-of-band from the recorded source_url and hand bytes to the extractor via manifest `local_path`; never disable verification.

## Corpus binding

`.axiom/toolchain.toml` pins the immutable signed corpus release this repository consumes (`bo-rulespec-2026-07-23`). The shared validate workflow verifies the release object signature, content hash, and waiver-set hash on every push.

## Layout

- `bo/statutes/`, `bo/regulations/`, `bo/policies/`: encoded RuleSpec modules with mandatory companion `.test.yaml` files.
- `programs/`: declarative compose specs (one per jurisdiction/program/period).
- `data/oracles/`, `data/coverage/`: comparison-oracle references and the BOLMOD instrument map. Never legal authority.

## Parity program

Tracked on issue #1: tranche-2 captures (post-2004 Ley 843 amendment instruments; DS 21531 RC-IVA reglamento and companion reglamentos; COVID-19 DS bonos 3546/4197/4200/4215/4345; program reglamentos operativos) and BOLMOD parity tests per instrument.

## Listing gates

This repo carries `app_visibility = "experimental"` in `.axiom/registry.toml` and stays out of app surfaces until:

1. The encoded surface covers the flagship calculation (the RC-IVA gross-to-net calculation for a formal employee) end to end with companion tests.
2. Oracle parity suites exist and pass against BOLMOD for the encoded surface.
3. Citation paths are stable (ley/decreto-number form against the Gaceta Oficial prints).
