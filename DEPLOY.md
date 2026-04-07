# Come deployare su GitHub Pages

Tre step. Ti servono ~2 minuti e nessun account a pagamento.

## Step 1 — Crea il repo pubblico su GitHub

1. Vai su <https://github.com/new>
2. Compila:
   - **Owner**: `alessandroplaca-uro`
   - **Repository name**: `voynich-visualization`
   - **Description** (opzionale): `Interactive 3D visualization of the Voynich morphemic system — Currier hand edition`
   - **Visibility**: ⚠️ **Public** (deve essere pubblico per Pages gratuito)
   - **Initialize this repository with**: lascia tutto SPENTO. NON aggiungere README, .gitignore, license — il repo locale ce li ha già.
3. Click **Create repository**.

## Step 2 — Pusha il repo locale

Questo repo locale è già inizializzato e ha un commit pronto. Dal terminale:

```bash
cd /home/user/voynich-visualization
git remote add origin https://github.com/alessandroplaca-uro/voynich-visualization.git
git push -u origin main
```

(Se ti chiede credenziali, usa il tuo token GitHub come password.)

## Step 3 — Attiva GitHub Pages

1. Vai su <https://github.com/alessandroplaca-uro/voynich-visualization/settings/pages>
2. Sotto **Build and deployment** → **Source**: scegli **Deploy from a branch**
3. **Branch**: `main`, **Folder**: `/ (root)`
4. Click **Save**.
5. Aspetta 30-60 secondi. Quando vedi il banner verde "Your site is live at..." è pronto.

L'URL sarà: <https://alessandroplaca-uro.github.io/voynich-visualization/>

## Aggiornamenti futuri

Quando vuoi aggiornare il visualizzatore:

1. Nel repo privato `voynich-memory`, rigenera l'HTML:
   ```bash
   python3 rupescissa/viz/generate_voynich_3d_v2.py
   ```
2. Copia l'output qui:
   ```bash
   cp /home/user/voynich-memory/rupescissa/viz/voynich_3d.html \
      /home/user/voynich-visualization/index.html
   ```
3. Commit + push:
   ```bash
   cd /home/user/voynich-visualization
   git add index.html
   git commit -m "Update viz: <descrizione>"
   git push
   ```

GitHub Pages si rebuilda automaticamente in 30-60 secondi.

## Note

- Il file `.nojekyll` (vuoto) dice a GitHub Pages di NON processare il sito
  con Jekyll. Necessario per file/cartelle che iniziano con `_`.
- L'HTML è self-contained: ~92 KB con tutti i dati embedded. Plotly viene
  caricato dal CDN al primo accesso.
- Niente backend, niente DB, niente API key. È un sito completamente statico.
