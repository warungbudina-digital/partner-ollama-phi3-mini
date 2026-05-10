# partner-ollama-phi3-mini

Partner ringan untuk klasifikasi, ekstraksi JSON, routing, dan ringkasan pendek.

## Tujuan

Repo ini adalah baseline partner khusus model **phi3:mini** untuk ekosistem OpenClaw + n8n Ayang. Fokusnya bukan membuat sistem besar di dalam repo, tapi memberi arah yang stabil, ringan, dan mudah dipakai pada **Google Cloud Shell gratis**.

## Prinsip desain

- kecil, cepat, dan murah dijalankan
- minim dependency tambahan
- tidak menyimpan artefak besar di repo
- cocok untuk sesi Cloud Shell yang ephemeral
- output harus mudah dipakai ulang oleh n8n

## Peran utama

- model: `phi3:mini`
- role: `triage-router-extractor`
- use in n8n: Classifier, router, extractor, first-pass sentiment/tagging node.

## Cocok untuk

- classify intent / task
- extract fields into strict JSON
- route jobs in n8n
- write short summaries and labels
- cheap first-pass filtering

## Hindari untuk

- long multi-file code generation
- heavy reasoning chains
- large context drafting
- deep architecture decisions

## Struktur awal

- `configs/partner.profile.json` — profil runtime dan guardrails partner
- `docs/CLOUD_SHELL_PROFILE.md` — batas desain agar tetap stabil di Cloud Shell gratis
- `docs/N8N_ROLE.md` — peran partner di workflow n8n
- `prompts/SYSTEM.md` — prompt sistem dasar partner
- `tasks/BACKLOG.md` — backlog implementasi awal
- `scripts/preflight.sh` — cek ringan sebelum dipakai di Cloud Shell

## Quick start

```bash
bash scripts/preflight.sh
cat configs/partner.profile.json
cat prompts/SYSTEM.md
```

## Catatan

Repo ini sengaja dibuat **tipis**. Di Cloud Shell gratis, kestabilan lebih penting daripada banyak fitur. Simpan logika berat di n8n/OpenClaw atau service remote, bukan di repo partner ini.


## Deploy bridge

Repo ini juga sudah punya baseline deploy ala `partner-AI` di:

- `deploy/ollama-fastapi/`

Isi folder itu menyediakan:
- Docker build untuk FastAPI bridge
- `docker-compose.yml` untuk Ollama + API + Cloudflared
- `.env.example`
- contoh config OpenClaw

Default model deploy untuk repo ini: **phi3:mini**
