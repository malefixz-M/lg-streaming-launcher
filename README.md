# LG Streaming Launcher – dominio dinamico

Questo repository mantiene aggiornato il dominio pubblicato nella pagina Telegraph e lo espone tramite GitHub Pages.

## Come funziona

1. GitHub Actions controlla periodicamente la pagina Telegraph.
2. Estrae il primo URL HTTPS il cui host contiene `streamingcommunity`.
3. Aggiorna `docs/latest.json`.
4. `docs/index.html` legge quel JSON e reindirizza il browser al dominio trovato.

**Importante:** questo repository aggiorna e pubblica il dominio. Da solo non può invocare `luna-send` sul televisore. Per il pulsante Luma che apre il browser nativo servirà anche un piccolo ponte locale sul TV (Luma può invocare un URL HTTP, ma un server cloud non può eseguire comandi sul televisore).

## Configurazione GitHub

1. Crea un repository GitHub chiamato `lg-streaming-launcher`.
2. Carica tutti i file di questa cartella mantenendo la struttura.
3. In **Settings → Pages**, imposta la pubblicazione da **Deploy from a branch**, branch `main`, cartella `/docs`.
4. In **Settings → Actions → General**, verifica che le workflow permissions consentano le azioni predefinite di lettura e scrittura dei contenuti. Il workflow dichiara già `contents: write`.
5. Vai in **Actions**, abilita i workflow se GitHub lo richiede, quindi esegui **Aggiorna dominio StreamingCommunity** con **Run workflow**.

La pagina sarà disponibile a:
`https://TUO-UTENTE.github.io/lg-streaming-launcher/`

Il JSON sarà disponibile a:
`https://TUO-UTENTE.github.io/lg-streaming-launcher/latest.json`

## Aggiornamento automatico

Il workflow è pianificato ogni 30 minuti. GitHub può ritardare l'esecuzione degli eventi `schedule`; il pulsante **Run workflow** consente un aggiornamento manuale.

## Sicurezza e limiti

- Nessun token personale GitHub è richiesto nel codice.
- Il workflow accetta solo URL HTTPS con un hostname contenente `streamingcommunity`.
- Il dominio è controllato al momento dell'aggiornamento, non ad ogni apertura.
- La pagina non incorpora player, contenuti o link a singoli video: si limita a reindirizzare al dominio pubblicato.
