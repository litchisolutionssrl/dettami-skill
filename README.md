# Dettami per Claude Code

Il marketplace di plugin di [Dettami](https://dettami.litchiserver.com), l'app di dettatura di Litchi Solutions, per
Claude Code. Contiene il plugin `dettami`, con la skill `/dettami-prompt`: trasforma una richiesta dettata in un prompt
da esperto per Claude Code, te lo mostra e chiede «Procedo così?» prima di eseguirlo. Il prompt lo scrive la tua
sessione di Claude Code, con il tuo abbonamento: niente chiavi API.

## Installazione

In Claude Code:

```
/plugin marketplace add litchisolutionssrl/dettami-skill
/plugin install dettami@dettami-skill
```

Dalla riga di comando: `claude plugin marketplace add litchisolutionssrl/dettami-skill`, poi
`claude plugin install dettami@dettami-skill`.

## Uso

```
/dettami-prompt [adatta|compatto|esteso] <testo dettato>
```

- `compatto`: poche righe, senza sezioni; `esteso`: sempre a sezioni (ruolo, obiettivo, contesto, metodo, criteri,
  vincoli, formato, cosa chiedere prima di agire); `adatta` (se non scrivi niente): secondo la richiesta.
- Il prompt è nella lingua del testo e non inventa niente: se manca qualcosa, dice di guardare il codice e di chiedere.
- Dettami lo incolla da solo quando, in Impostazioni › Formattazione, scegli «Claude Code (il mio abbonamento)»:
  <!-- versione-app -->l'opzione arriva con la prossima versione di Dettami.<!-- /versione-app -->
- Con altri comandi che si chiamano allo stesso modo, si usa la forma completa `/dettami:dettami-prompt`.

Licenza MIT (`LICENSE`).

---

# Dettami for Claude Code

The Claude Code plugin marketplace of [Dettami](https://dettami.litchiserver.com), the dictation app by Litchi
Solutions. Its `dettami` plugin adds `/dettami-prompt`: it turns a dictated request into an expert prompt for Claude
Code, shows it and asks before carrying it out. Your own Claude Code session writes the prompt: no API key needed.

Install with `/plugin marketplace add litchisolutionssrl/dettami-skill`, then `/plugin install dettami@dettami-skill`.
Use: `/dettami-prompt [adatta|compatto|esteso] <dictated text>`. Dettami pastes it for you when you choose «Claude Code (il
mio abbonamento)» in Settings › Formatting: <!-- version-app -->the option comes with the next Dettami version.<!-- /version-app -->

MIT License (`LICENSE`).
