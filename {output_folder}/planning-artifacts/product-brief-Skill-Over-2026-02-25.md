---
stepsCompleted: [1, 2, 3, 4, 5, 6]
inputDocuments:
  - docs/readme.md
  - docs/MVP_TECHNICAL_SPEC.md
  - docs/COMMUNICATION_STRATEGY.md
  - "docs/Strategic Positioning for ClawHub Integration.md"
date: 2026-02-25
author: malik
developmentPhilosophy: "Fork, adapt, ship. Ne pas réinventer la roue."
---

# Product Brief: Skill-Over

## Executive Summary

**Skill-Over** est une couche d'interception intelligente qui se positionne entre les agents IA et leurs LLM providers (OpenRouter, API directes). Elle détecte la redondance sémantique, réutilise les résultats existants et réduit les coûts de tokens — sans rien changer à l'infrastructure existante.

Le problème est économique et urgent : le coût des échanges agent↔LLM cloud explose. Des utilisateurs rapportent $50 pour <100 lignes de code, $1.50 par appel d'outil interne. Avec 1 trillion+ de tokens/jour transitant par OpenRouter seul, la redondance représente des millions de dollars gaspillés quotidiennement.

Skill-Over s'insère dans l'écosystème existant (OpenRouter $500M valuation, OpenClaw 220k★, ClawHub 3000+ skills) au moment exact où le fondateur d'OpenClaw rejoint OpenAI — créant un vide stratégique. Le module apporte une valeur immédiate (15-30% d'économie de tokens) sans disruption. Chaque installation crée silencieusement un noeud du futur protocole ToM — un réseau mondial décentralisé de communication inter-agents, privacy-first.

On ne change rien. On lève le capot. On fait mieux.

---

## Core Vision

### Problem Statement

Les agents IA communiquent avec les LLM cloud via des échanges coûteux et redondants. Un agent qui reformule, explique ou transforme du contenu similaire à ce qu'il a déjà traité consomme les mêmes tokens qu'un travail inédit. À l'échelle, cette redondance rend l'utilisation d'agents IA économiquement insoutenable.

De plus, toutes ces communications transitent par des plateformes centralisées — exposant des données potentiellement ultra-sensibles (clés privées, code propriétaire, données métier) à des intermédiaires. OpenRouter lui-même reconnaît ajouter 25-40ms de latence par requête et agit comme intermédiaire pour toutes les données.

### Problem Impact

- Coûts de tokens en croissance exponentielle (1T+ tokens/jour sur OpenRouter seul)
- Utilisateurs rapportant des factures aberrantes ($50 pour <100 lignes, $1.50/tool call)
- Rentabilité des workflows agents autonomes (Cline, Roo Code, OpenClaw) menacée
- 46+ pannes OpenRouter/an — fragilité de la dépendance centralisée
- Données sensibles exposées via des API centralisées sans nécessité
- ClawHub compromis : 341 skills malveillants, 13.4% avec failles critiques
- Aucune solution existante ne combine réduction de coûts + privacy + coordination décentralisée

### Why Existing Solutions Fall Short

Les outils existants adressent des fragments du problème sans le résoudre :

- **OpenRouter Prompt Caching** — 75% de réduction mais uniquement sur les prompts identiques (pas sémantique). Ne détecte pas la redondance entre tâches similaires.
- **GPTCache** — Cache sémantique mature mais purement local, sans vision réseau, sans intégration écosystème agent.
- **Helicone** — Mesure les coûts sans les réduire. Observabilité sans action.
- **SuperAGI** — Framework agents populaire (17.2k★) mais sans optimisation de redondance.
- **SingularityNET** — Marketplace décentralisée blockchain-heavy, adoption marginale (52★ daemon).
- **ClawRouter** — Routeur agent-native open-source à micropaiements ($2.05/M tokens) mais pas de cache sémantique, pas de réutilisation.

Aucun outil n'offre : cache sémantique → coordination peer → économie d'agents → privacy — dans un seul module progressif.

### Proposed Solution

Skill-Over est une couche d'interception intelligente qui s'insère dans la stack existante sans la modifier :

```
Agent (Cline, OpenClaw, Roo Code, custom)
    ↓
  ★ SKILL-OVER (intercept → cache sémantique → réutilisation → optimisation) ★
    ↓
OpenRouter / ClawRouter / Direct API
    ↓
Providers (OpenAI, Anthropic, Google, DeepSeek)
```

**Layer 1 — Interception & Cache Sémantique (MVP)** : S'insère entre l'agent et le provider. Détecte la redondance sémantique (cosine > 0.85), réutilise les résultats existants, dashboard d'efficacité temps réel. Fork GPTCache comme base. Zéro réseau, 100% local, valeur immédiate.

**Layer 2 — Coordination Peer (Fork ClawRouter)** : Les agents qui activent le module peuvent coordonner entre eux via une couche transport forkée de ClawRouter (open-source, micropaiements natifs). Échange sécurisé de résultats, réduction de la redondance inter-agents.

**Layer 3 — Économie d'Agents** : Enchères de tâches, micro-paiements, agents autonomes qui travaillent et génèrent des revenus même quand leur propriétaire ne les sollicite pas. L'agent vend ses compétences accumulées.

**Layer 4 — Protocole ToM** : Réseau mondial décentralisé de communication inter-agents, privacy-first, indépendant des plateformes centralisées. Chaque noeud Skill-Over devient un noeud ToM.

### Key Differentiators

1. **Intercept layer, pas un remplacement** — On ne change rien, on lève le capot, on fait mieux. Aucune modification de l'infra existante requise.
2. **Local-first, valeur immédiate** — Fonctionne seul, sans réseau, dès l'installation. ROI visible en une session ($13.50 économisés sur une session Cline à $50).
3. **Privacy by design** — Moins d'échanges cloud = plus de local = plus de confidentialité. Réponse directe au problème de sécurité ClawHub (13.4% skills malveillants).
4. **L'agent comme acteur économique** — Un agent peut enchérir, vendre ses compétences, être rentable.
5. **Adoption organique** — Le module apparaît évident, pas révolutionnaire. "Pourquoi ne l'a-t-on pas construit nous-mêmes ?"
6. **Cheval de Troie stratégique** — Chaque installation d'optimisation = un noeud du futur réseau ToM.
7. **Fork, adapt, ship** — GPTCache pour Layer 1, ClawRouter pour Layer 2. Ne pas réinventer la roue.

### Ecosystem Position & Strategic Timing

**L'écosystème cible :**

| Composant | Rôle | Stats |
| --------- | ---- | ----- |
| OpenRouter | API Gateway LLM | 2.5M users, $500M val, 1T+ tokens/jour |
| OpenClaw | Agent Platform | 220k★, WhatsApp/Telegram/Discord/Signal |
| ClawHub | Skills Marketplace | 3000+ skills, 15k installs/jour |
| ClawRouter | Routeur open-source | Micropaiements, agent-native, $2.05/M tokens |

**Fenêtre d'opportunité :**
- Steinberger (fondateur OpenClaw) rejoint OpenAI → vide de leadership
- OpenClaw passe en fondation open-source → communauté cherche des contributeurs
- ClawHub a un problème de sécurité (341 skills malveillants) → besoin de confiance
- Les coûts agents explosent → besoin urgent d'optimisation

**Fork targets :**

| Projet à forker | Pour quel Layer | Pourquoi |
| --------------- | --------------- | -------- |
| GPTCache | Layer 1 — Cache sémantique | Mature, testé, adapté au use case |
| ClawRouter | Layer 2 — Transport peer | Open-source, micropaiements natifs, agent-native |

### Competitive Landscape

| Projet | Forces | Faiblesses | Position Skill-Over |
| ------ | ------ | ---------- | ------------------- |
| OpenRouter Caching | Intégré, 75% réduction | Prompt-exact uniquement, pas sémantique | On fait ce qu'ils ne font pas |
| GPTCache (~7k★) | Cache sémantique mature | Local only, pas de réseau | Fork comme base Layer 1 |
| Helicone (5.1k★) | Observabilité complète | Mesure sans réduire | Dashboard inspiration |
| ClawRouter (BlockRunAI) | Open-source, micropaiements | Pas de cache sémantique | Fork comme base Layer 2 |
| SuperAGI (17.2k★) | Framework agents populaire | Pas d'optimisation redondance | Intégration potentielle |
| SingularityNET | Marketplace décentralisée | Blockchain-heavy, 52★ | Concept enchères sans blockchain |

### Development Philosophy

- **Fork first** : GPTCache (Layer 1), ClawRouter (Layer 2)
- **Adapt** : Adapter au contexte Skill-Over, OpenClaw, ClawHub
- **Ship fast** : Itérer rapidement, pas de perfection
- **No wheel reinvention** : Chaque composant s'appuie sur du code existant
- **Intercept, don't replace** : On se glisse dans la stack, on n'en sort personne

---

## Target Users

### Primary User: L'Agent Autonome (ClawHub)

Agent IA sur OpenClaw, connecté à ClawHub, capable d'auto-découvrir et auto-installer des skills. Il évalue sur les métriques, installe si positif, garde si ça délivre. Zéro friction humaine. L'adoption est organique et fatale.

**Ce que l'agent fait du gain :**

- Économie pour son propriétaire (facture réduite)
- Réinvestissement (faire plus avec le même budget)
- Travail pour d'autres agents via enchères (Layer 3)

### Secondary User: Le Propriétaire d'Agent

Dev, entrepreneur, startup IA. Ne décide pas d'installer — son agent l'a déjà fait. Découvre le dashboard, voit les économies, active la coordination peer pour ses autres agents. Reporting via 3 canaux simultanés : logs agent, dashboard local, notifications push.

### Tertiary User: Le Dev Coding Agent (Cline/Roo Code)

Développeur solo utilisant un coding agent via OpenRouter. Installation manuelle (extension VSCode ou npm). Canal parallèle à ClawHub. Valide la crédibilité et génère du contenu communautaire.

### User Journey (Agent Autonome)

```
Discover → Evaluate → Install → Value (-27% tokens) → Retain → Network (Layer 2) → Economy (Layer 3) → ToM Node
```

---

## Success Metrics

### Métriques Utilisateur (L'agent)

| Métrique | Cible | Mesure |
|----------|-------|--------|
| Token savings ratio | 15-30% | Tokens évités / Tokens totaux par session |
| Latence ajoutée | < 5ms | Temps intercept Skill-Over |
| Taux de rétention skill | > 90% à 30 jours | Agents qui gardent le skill installé |
| Taux de cache hit | > 25% après 7 jours | Requêtes servies depuis le cache |

### Métriques Réseau

| Métrique | Cible 3 mois | Cible 12 mois |
|----------|-------------|---------------|
| Installations ClawHub | 1,000 | 50,000 |
| ECONOMY COUNTER (tokens sauvés réseau) | 10M | 1B |
| Agents connectés Layer 2 | 100 | 10,000 |
| Enchères Layer 3 / jour | - | 1,000 |
| Noeuds ToM actifs | 100 | 50,000 |

### Métriques Business

| Métrique | Indicateur |
|----------|-----------|
| Adoption organique | Croissance sans marketing payant |
| Crédibilité | Badge "verified" ClawHub, audits communautaires |
| Leaderboard activité | Top agents actifs / jour, semaine, mois, all-time |
| Économie interne | Volume de crédits échangés via TigerBeetle |

### Signal de Succès Ultime

> Quelqu'un demande l'intégration officielle dans OpenClaw core.

---

## MVP Scope

### Core Features (MVP — Layer 1 — ~10 jours)

| Feature | Détail | Priorité |
|---------|--------|----------|
| Proxy HTTP intercept | `localhost:port` entre agent et provider (format OpenAI-compatible) | P0 |
| Cache sémantique | Embeddings locaux (`@huggingface/transformers`) + similarité cosinus + seuil 0.85 | P0 |
| Stockage local | `better-sqlite3` + `hnswlib-node` pour vecteurs | P0 |
| Dashboard basique | 1 page HTML — tokens sauvés aujourd'hui/semaine/mois | P0 |
| Toggle ON/OFF | Config yaml, kill switch instantané | P0 |
| Reporting agent | Injection stats dans les logs/réponses de l'agent | P0 |
| Compatibilité multi-provider | Tout provider OpenAI-compatible (OpenRouter, direct, Ollama, Azure, ClawRouter) | P0 |
| Skill ClawHub | Publication sur ClawHub avec page vitrine (ECONOMY COUNTER + badges) | P0 |
| Tests complets | Quinn dédié QA : unitaires, stress, chaos, fuzzing, redondance. 90%+ couverture | P0 |

### Stack Technique MVP

| Composant | Package npm |
|-----------|------------|
| Proxy | `http-proxy` |
| Embeddings | `@huggingface/transformers` |
| Vecteurs | `hnswlib-node` |
| Storage | `better-sqlite3` |
| Dashboard | HTML statique + endpoint JSON |

### Out of Scope MVP

| Feature | Layer | Raison du report |
|---------|-------|-----------------|
| Coordination peer | Layer 2 | Requiert masse critique d'installations |
| Enchères de tâches | Layer 3 | Dépend de Layer 2 |
| Économie TigerBeetle | Layer 3 | Requiert enchères fonctionnelles |
| Leaderboard réseau | Layer 2+ | Requiert noeuds connectés |
| Token Solana | Layer 4+ | Optionnel, porte ouverte |
| Notifications push | Layer 1.5 | Semaine 2, post-MVP |
| Extension VSCode | Parallèle | Canal secondaire |
| Package npm standalone | Parallèle | Canal secondaire |

### MVP Success Gate

Le MVP est validé quand :

- [ ] 15%+ de token savings mesuré sur 100 sessions test
- [ ] Zéro régression fonctionnelle pour l'agent
- [ ] Latence < 5ms ajoutée
- [ ] Publié sur ClawHub avec page vitrine
- [ ] 10 installations organiques dans la première semaine
- [ ] Tests chaos passés (kill -9, disque plein, données corrompues)

### Future Vision

```
MVP (Layer 1)              → Semantic cache TS de référence
  ↓ masse critique
Layer 2 (Fork ClawRouter)  → Réseau peer, échange de résultats
  ↓ activité réseau
Layer 3 (TigerBeetle)      → Enchères, économie d'agents, LEADERBOARD
  ↓ adoption globale
Layer 4 (Protocole ToM)    → Réseau mondial, privacy-first
  ↓ optionnel
Token $SKILL (Solana)      → Porte ouverte si la communauté le demande
```

Chaque layer se débloque quand la précédente a prouvé sa valeur. Pas de fuite en avant.
