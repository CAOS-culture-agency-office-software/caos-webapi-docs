# 📄 CHANGELOG

All notable changes to this project will be documented in this file.

This project follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) and uses [semantic versioning](https://semver.org/).

---

## [1.2.0] – 2025-07-16
### Added
- New optional fields added to webhook payload and data model:
  - `tickets_advancesale_internet_date_event`
  - `tickets_advancesale_phone_date_event`
  - `tickets_advancesale_start_date_event`
  - `info_text_date_event`
  - `venue_name_date_event`
- JSON example updated accordingly in webhook specification
- Data model extended with new fields and descriptions

---

## [1.1.0] – 2025-06-25
### Added
- New optional fields added to webhook payload:
  - `time_catering`
  - `time_curfew`
  - `time_pause`
  - `time_photosession`
  - `time_showende`
- Field table updated accordingly in webhook specification
- JSON example extended with new fields

---

## [1.0.0] – 2025-06-24
### Added
- Initial publication of CAOS WebAPI documentation
- Markdown files for:
  - Webhook specification
  - Data model
  - ER diagram
  - Project README
