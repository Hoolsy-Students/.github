# CLAUDE.md — .github

## Formål
Delte GitHub Actions workflows, issue- og PR-maler, og orgens offentlige
profil.

## Skal ikke inneholde
- Applikasjonskode.
- Tjenester eller pakker.
- Enkeltrepos konfigurasjon — den ligger i det aktuelle repoet.

## Struktur
- `profile/README.md` — orgens offentlige presentasjon
  (https://github.com/HoolsyAS). Rører ikke uten produkteierens
  godkjenning.
- `.github/workflows/` — reusable workflows kalt fra andre repoer.
- `ISSUE_TEMPLATE/`, `PULL_REQUEST_TEMPLATE.md` — delte maler.
- `CODEOWNERS` — reglene som gjelder for dette repoet selv.

## Grenser
- Endringer i reusable workflows treffer alle repoer og behandles som
  infra-endring: PR med review fra `infra`.
- Reusable workflows må være bakoverkompatible innenfor samme major
  version. Nye krav bumpes til ny major.

## Konvensjoner
### Mappestruktur
- Én workflow-fil per formål, ikke per repo som kaller den.

### Navngiving
- Kebab-case for workflow-filnavn.
- Prefiks `reusable-<formål>.yml` for kallbare workflows.

### Testkrav
- Workflow-endringer verifiseres ved kall fra minst ett faktisk repo
  før merge til main.

## Felles regler for alle Hoolsy-repoer

<!-- Synkronisert fra hoolsy-docs/conventions.md. Ikke rediger her.
Endringer gjøres i hoolsy-docs og synkes ut. -->

- `hoolsy-contracts` er eneste delte avhengighet på tvers av repoer.
  Ingen repo importerer typer fra et annet repo.
- Ingen delt database mellom tjenester. Kryssoppslag via API eller
  hendelsesdrevne lesemodeller.
- Eksterne APIer og modellinferens hører i berikelsesløpet, aldri i
  konsumentens leseløp.
- Hvert objekt bærer provenance: kilde, versjon, konfidens.
- Artefakt er en gyldig tilstand, ikke en feil.
- Manuell berikelse vinner over AI, men overskriver ikke. Begge lag
  bevares. Samme presedensregel overalt der to kilder er uenige.
- Gjenkjenningskontrakten er
  `{ content_id, position_ms, confidence, lane, playback_state? }`.
- Objekter har tre tidspunkter: `visible_from`, `visible_to` og
  `display_until`. `display_until = visible_to + 10s`, beregnes én
  gang i `graph` og ligger i dataene klienten får. Ingen flate
  beregner den selv.
- Engelsk i kode, identifikatorer, skjemaer, commit-meldinger og
  PR-titler. Norsk kun i ADR-prosa og produktdokumentasjon.
