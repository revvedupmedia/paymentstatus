# Payment Status Pages — bcl.MY

Retro pixel-art receipt pages untuk redirect dari **BCL.my Forms Payment** (Bayarcash). Hosted on GitHub Pages.

## Pages

| File | Purpose | Theme |
|------|---------|-------|
| `index.html` | Preview/test landing for all 3 pages | Green |
| `success.html` | Payment berjaya — access granted | Green |
| `failed.html` | Payment gagal — retry option | Red |
| `pending.html` | Payment processing — auto-refresh | Orange |

## Setup GitHub Pages

1. **Buat repo baru** di GitHub: `paymentstatus` (Public).
2. **Push files ni** ke repo:
   ```
   index.html
   success.html
   failed.html
   pending.html
   README.md
   ```
3. Buka **Settings → Pages**.
4. Source: **Deploy from a branch**.
5. Branch: **main** / folder: **/ (root)** → **Save**.
6. Tunggu 1-2 minit, page akan live di:
   ```
   https://revvedupmedia.github.io/paymentstatus/
   ```

## BCL.my Configuration

Dalam BCL.my dashboard → **Forms Payment → Advanced Settings → Redirect Receipt Page**, masukkan:

**Success URL:**
```
https://revvedupmedia.github.io/paymentstatus/success.html?order_number={order_number}&amount={amount}&transaction_id={transaction_id}&payment_date={payment_date}&payer_name={payer_name}&payer_email={payer_email}
```

> Success page ada button **LOGIN HOOKCRAFT** → `https://hookcraft.net/auth` dan button **WHATSAPP ADMIN** (`+60 11-1107 1083`) yang auto-isi mesej dengan nama, email, order, amount, txn ID — admin boleh confirm akses cepat.

**Failed URL:**
```
https://revvedupmedia.github.io/paymentstatus/failed.html?order_number={order_number}&amount={amount}&reason={status}
```

**Pending URL:**
```
https://revvedupmedia.github.io/paymentstatus/pending.html?order_number={order_number}&amount={amount}&payment_method={payment_method}
```

## URL Variables yang Disokong

Pages akan auto-parse query string dari BCL.my redirect:

- `order_number` — Order ID
- `amount` — Jumlah (auto-format ke RM xx.xx)
- `status` — Status pembayaran (auto-uppercase)
- `transaction_id` — Transaction reference
- `payment_date` — Tarikh transaksi
- `payment_method` — Method (FPX, card, dll)
- `reason` — Sebab gagal (failed page only)

Kalau parameter tak diset, page akan papar fallback default (e.g. `--` atau tarikh hari ini).

## Local Preview

Buka `index.html` dalam browser, atau guna live server:
```bash
npx serve .
```

## Deploy via Git

```bash
cd "F:/landing page"
git init
git add index.html success.html failed.html pending.html README.md
git commit -m "Initial payment status pages"
git branch -M main
git remote add origin https://github.com/revvedupmedia/paymentstatus.git
git push -u origin main
```
