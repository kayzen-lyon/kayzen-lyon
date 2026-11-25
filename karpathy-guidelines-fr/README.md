# Consignes Karpathy — version française KAYZEN

Skill pour Claude (Claude Code et claude.ai) qui réduit les erreurs courantes des LLM quand ils codent : suppositions silencieuses, code trop compliqué, modifications hors sujet, tâches déclarées finies sans vérification.

Version française et enrichie du skill [`karpathy-guidelines`](https://github.com/forrestchang/andrej-karpathy-skills) de forrestchang, lui-même dérivé des [observations d'Andrej Karpathy](https://x.com/karpathy/status/2015883857489522876). Ce n'est pas une publication d'Andrej Karpathy.

## Ce qui change par rapport à l'original

- Traduit en français.
- **Lire avant d'écrire** : consulter le `CLAUDE.md` du projet, les exports et les appelants du fichier touché.
- **Quand demander** : s'arrêter seulement si une mauvaise supposition serait difficile à repérer (dates, unités, devises, règles métier, textes juridiques) ; sinon énoncer l'hypothèse et avancer.
- **Minimal ne veut pas dire fragile** : les entrées invalides réalistes sont rejetées ou signalées, jamais transmises en silence.
- **Test de régression** sur chaque correction de bug quand le projet a un outil de test ; pas d'autres tests non demandés.
- **Échouer bruyamment** et faire un point « fait / vérifié / reste » à chaque étape.
- **Règles KAYZEN** : zéro coût caché, indépendance vis-à-vis de l'hébergeur, accord explicite pour la production client, conformité et SEO, secrets, travail sur plusieurs postes Windows, produits IA.

Ces ajouts tiennent compte du [test publié par AI Parabellum](https://aiparabellum.com/) le 1er novembre 2026 (24 essais avec et sans le fichier d'origine).

## Installation

**Claude Code :** copier le dossier [`karpathy-guidelines/`](karpathy-guidelines) dans `~/.claude/skills/` (pour tous les projets) ou dans `.claude/skills/` d'un projet.

**claude.ai :** zipper le dossier `karpathy-guidelines/`, puis l'importer depuis les réglages des skills.

La section 5 « Règles KAYZEN » est propre à notre agence : adaptez-la ou supprimez-la pour votre usage.

## Licence

MIT — voir [LICENSE](LICENSE). Travail dérivé de forrestchang/andrej-karpathy-skills (MIT).

---
Publié par [KAYZEN](https://kayzen-lyon.com) — agence web à Lyon.
