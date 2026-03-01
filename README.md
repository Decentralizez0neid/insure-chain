# InsureChain

InsureChain adalah protokol perlindungan sosial terdesentralisasi berbasis Mutual Aid (dana bersama). Proyek ini memadukan deteksi sensor (DePIN), verifikasi warga (Tier 1 Pathfinder), dan investigasi juri anonim (Tier 2 Guardian) untuk menyederhanakan dan mempercepat pencairan dana solidaritas.

## Elevator Pitch
InsureChain memungkinkan komunitas lokal membangun pool likuiditas bersama untuk bantuan cepat setelah insiden — tanpa model asuransi tradisional. Validasi insiden menggunakan kombinasi: data sensor mobile (DePIN), kesaksian lokal, dan konsensus juri independen.

## Penempatan Regulasi & Terminologi (Legal‑Safe)
- Membership Contribution: iuran partisipasi untuk bergabung dalam perlindungan komunitas.
- Protection Status: status keanggotaan aktif yang tercatat di smart contract.
- Aid Request: permohonan pencairan dana solidaritas pasca‑insiden.
- Community Aid: dana bantuan yang dicairkan dari Liquidity Pool.

> Posisi legal: platform urun dana komunitas (mutual aid), bukan produk asuransi komersial. Dokumentasi hukum terpisah disarankan.

## Aktor Ekosistem
- Protector (Member): pengguna yang membayar kontribusi untuk perlindungan.
- Liquidity Provider (LP): penyedia modal awal dan pembiayaan pool.
- Pathfinder (Tier 1 Verifier): saksi/simpatisan lokal yang memberi sinyal awal.
- Guardian (Tier 2 Jury): investigator anonim yang melakukan deliberasi dan voting.
- Superadmin: tim internal untuk monitoring (dashboard Next.js).

## Arsitektur Ringkas (MVP)
- Blockchain Layer (Agnostic): smart contract EVM/SVM‑compatible sebagai vault, pencatatan incident flag, dan settlement voting.
- Mobile Layer (Flutter): pembacaan DePIN (G‑Force, GPS), UI verifikasi Pathfinder, Deliberation Room untuk Guardian.
- Backend & API (Golang): ingestion sensor, anti‑spam filter, query spasial, relayer gasless, background worker, dan chat/deliberation off‑chain.
- Web (Next.js): Superadmin dashboard untuk analitik, health pool, dan log insiden.
- Database (MySQL): penyimpanan off‑chain (incidents, verifications, chat logs) dengan index spasial.

## Alur Kerja MVP (Singkat)
1. Capitalization: LP menyetor modal ke smart contract → TVL awal tersedia untuk Community Aid.
2. Deteksi (DePIN): aplikasi Protector deteksi anomali (mis. hentakan G‑Force). Data dikirim ke Backend Go.
3. Tier 1 (H+0–H+1): Backend query spasial untuk mencari Pathfinder terdekat → kirim push notification → Pathfinder buka app dan pilih YES/NO → backend bertindak sebagai relayer untuk mencatat jawaban on‑chain tanpa biaya bagi Pathfinder.
4. Masa Tenang (H+1–H+24): Background worker memantau umur incident; setelah ambang waktu, sistem mengacak dan memilih Guardian.
5. Tier 2 (H+24): Guardian deliberasi di Deliberation Room (evidence bundle + Tier1 results) → vote Approve/Reject → vote difinalisasi on‑chain.
6. Settlement: jika mayoritas Approve, smart contract membayar Community Aid ke wallet korban; Guardian yang sejalan dengan mayoritas mendapat reward (Schelling reward mechanism).

## Nilai Jual Utama
- Frictionless Web3 UX: seluruh proses partisipasi (verifikasi & voting) dilakukan lewat mobile app tanpa memaksa pengguna memegang gas.
- Progressive Decentralization: beban chat/filtrasi off‑chain untuk efisiensi; keputusan keuangan final di smart contract.
- Separation of Concerns: mobile untuk partisipasi, backend untuk relayer dan filter, web dashboard untuk monitoring.

## Keamanan & Privasi (Ringkas)
- Minimalkan PII on‑chain; gunakan pseudonim untuk Guardian.
- Batasi akses bukti dan gunakan retention policy di DB.
- Smart contract: timelock, circuit breakers, dan audit security sebelum rilis.
- Backend: rate limiting, anomaly detection, dan heuristik anti‑fraud.

## KPI MVP (Contoh)
- End‑to‑settlement ≤ 48 jam (target pilot ≥ 90% kasus).
- Tier‑1 signal precision ≥ 85% pada dataset pilot.
- Guardian consensus final on‑chain ≤ 12 jam setelah pemilihan.

## Next Steps / Roadmap Singkat
1. Finalisasi PRD dan checklist pilot lapangan.
2. Scaffold repo: smart contract minimal (vault + incident flag), backend Go skeleton, Flutter starter, Next.js dashboard skeleton.
3. Buat incident simulator untuk menguji alur end‑to‑end.
4. Pilot internal dengan 100–200 pengguna untuk mengumpulkan telemetry.

## Cara kontribusi / kontak
Silakan buka issue atau PR di repo ini untuk fitur, bug, atau diskusi arsitektur.
