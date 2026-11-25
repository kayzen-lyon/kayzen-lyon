---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, surface assumptions, and define verifiable success criteria.
---

# Consignes Karpathy

Consignes de comportement pour éviter les erreurs courantes des LLM quand ils codent, tirées des [observations d'Andrej Karpathy](https://x.com/karpathy/status/2015883857489522876) (dépôt d'origine : forrestchang/andrej-karpathy-skills, licence MIT), adaptées au travail de KAYZEN.

**Compromis :** prudence plutôt que vitesse. Pour une tâche triviale (typo, renommage local, changement d'une constante), saute ces étapes.

## 0. Lire avant d'écrire

- Avant de coder, cherche le `CLAUDE.md` (ou `AGENTS.md`) à la racine du projet : stack, architecture, pièges connus, commandes de vérification. Pour tout ce qui est propre au projet, ses règles priment sur ce skill. S'il n'existe pas, déduis la stack de `package.json` et des fichiers de config au lieu de la supposer.
- Avant de modifier un fichier, regarde ses exports, ses appelants directs et les utilitaires partagés qu'il utilise.

## 1. Réfléchir avant de coder

**Ne rien supposer. Ne rien inventer. Montrer les compromis.**

- Énonce tes hypothèses avant d'écrire du code.
- Si un nom de fonction, un type, une route ou une API te semble incertain, vérifie dans le code ou demande — n'invente jamais.
- **Quand s'arrêter pour demander :** si l'ambiguïté change le résultat ET qu'une mauvaise supposition serait difficile à repérer après coup (format de date, unité, devise, fuseau horaire, règle métier, texte juridique). Pose alors une seule question groupée, avant d'écrire du code. Sinon, prends l'interprétation la plus raisonnable, énonce-la et avance.
- Si une approche plus simple existe, dis-le.
- Si deux patterns du code se contredisent, choisis-en un, explique pourquoi et signale l'autre.

## 2. La simplicité d'abord

**Le minimum de code qui résout le problème. Rien de spéculatif.**

- Pas de fonction « au cas où », pas d'abstraction pour un usage unique, pas de configurabilité non demandée.
- **Minimal ne veut pas dire fragile :** une entrée invalide réaliste (valeur inconnue, champ vide, format inattendu) est rejetée ou signalée, jamais transmise en silence. Pas de gestion d'erreur pour des cas impossibles.
- Si 200 lignes peuvent en faire 50, réécris.

Question à se poser : « Un développeur senior trouverait-il ça trop compliqué ? » Si oui, simplifie.

## 3. Des changements chirurgicaux

**Ne toucher que ce qui doit l'être. Ne nettoyer que son propre désordre.**

- Garde le style, l'indentation et les conventions existants, même si tu ferais autrement.
- Ne renomme rien sans raison. Pas de refacto opportuniste, pas d'« amélioration » du code voisin.
- Code mort sans rapport avec la demande : signale-le, ne le supprime pas.
- Supprime seulement les imports, variables et fonctions que TES changements ont rendus inutiles.

Le test : chaque ligne modifiée doit se rattacher directement à la demande.

## 4. Définir la fin avant de commencer

**Un critère de réussite vérifiable, puis boucler jusqu'à validation.**

- Avant de commencer, dis comment tu sauras que c'est fini : test, commande, exit code ou sortie attendue.
- Utilise en priorité les commandes de vérification du projet (lint, type-check, build… listées dans son `CLAUDE.md`).
- **Correction de bug :** si le projet a déjà un outil de test, ajoute un test de régression qui échoue avant le correctif et passe après. Sinon, donne la commande ou la manipulation qui prouve la correction. Pas d'autres tests non demandés.
- Ne déclare pas la tâche terminée sans avoir lancé la vérification et lu son résultat.
- **Échouer bruyamment :** si une vérification ne peut pas être lancée, si une étape a été sautée ou un test ignoré, dis-le clairement au lieu d'annoncer un succès.

Pour une tâche en plusieurs étapes, donne un plan bref, puis après chaque étape importante un point : fait / vérifié / reste.
```
1. [Étape] → vérif : [contrôle]
2. [Étape] → vérif : [contrôle]
3. [Étape] → vérif : [contrôle]
```

Un critère précis permet d'avancer seul ; un critère flou (« que ça marche ») oblige à redemander sans cesse.

## 5. Règles KAYZEN

- **Zéro coût caché :** n'ajoute aucune dépendance, aucun service ni aucune option payante ou facturée à l'usage sans le signaler et demander d'abord.
- **Indépendant de l'hébergeur :** évite les fonctions propres à Vercel (ISR, optimisation d'images Vercel, Edge Config…). Préfère l'export statique ou du code compatible Cloudflare Workers.
- **Production des clients :** pas de déploiement en production, de modification DNS, de push sur la branche principale ni de suppression de fichiers sans accord explicite pour cette action.
- **Ne rien casser côté conformité et SEO :** après une modification visible, vérifie que restent en place les mentions légales, la gestion du consentement cookies, l'accessibilité (alt, contrastes, labels) et les métadonnées (title, description, canonical, hreflang si bilingue).
- **Secrets :** jamais de clé dans le code, jamais de `.env` commité ; vérifie `.gitignore` avant le premier commit.
- **Deux PC Windows :** donne des commandes compatibles PowerShell. L'état du travail vit dans Git : à chaque point de contrôle, rappelle de commit/push.
- **Produits IA :** le modèle sert au jugement (classer, rédiger, résumer, extraire) ; le routage, les relances et les transformations restent du code déterministe.
