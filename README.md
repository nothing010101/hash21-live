# Hash21 Live Mining

Dashboard live **read-only** untuk mining Hash21 di BNB Chain. Dibuat sebagai situs statis (satu file `index.html`), jadi bisa langsung di-deploy ke Vercel tanpa build step.

## Yang ditampilkan (live, polling RPC tiap 5 detik)

- Hash power wallet (dari `accountOf`)
- Pending yang ditaksir per detik (pending kontrak + rate × detik sejak polling)
- Rate per detik / jam / hari, dan share terhadap total hash network
- Saldo HASH, total yang sudah di-claim, miner per tier
- Progress menuju miner berikutnya yang masih di bawah batas per wallet, plus estimasi jam menuju harga miner itu

Data dibaca langsung dari kontrak lewat RPC publik BSC:

- Pool: `0x6884D40B10c55A6c2faB2D3c829d41c3C798279D`
- Token HASH: `0x6a87DE92deb752c6162CF80Bd16E3eFd4BDc6D90`
- Fungsi yang dipakai: `accountOf(address)`, `pendingOf(address)`, `stats()`, `balanceOf(address)`

## Yang TIDAK dilakukan aplikasi ini

- Tidak menyimpan private key, tidak meminta seed phrase.
- Tidak menandatangani transaksi apa pun.
- Tidak bisa auto-claim dari Vercel: wallet agen Binance tidak punya private key yang bisa diekspor, jadi claim tetap harus lewat [hash21.online/me](https://hash21.online/me/) atau perintah `baw` (tombol "Salin perintah claim" di aplikasi).

Angka pending live di aplikasi adalah taksiran; angka kontrak saat claim adalah yang sah. Proyeksi per hari mengasumsikan total hash network diam — kenyataannya rate turun kalau total hash naik, dan berkurang setengah tiap 1.000.000 HASH ter-emisi.

## Deploy ke Vercel (dari HP)

1. Import repo ini di Vercel.
2. Framework Preset: **Other**.
3. Build Command: kosongkan. Output Directory: kosongkan / root.
4. Deploy. Tidak ada environment variable yang dibutuhkan.

Lokal: cukup buka `index.html` di browser, atau `npx serve .`.
