# SESSION HANDOFF — État complet au 10 juin 2026
> À charger en début de nouvelle conversation Claude Cowork
> Auteur : Samuel Gomis + Claude Cowork

---

## RÉSUMÉ DE LA MEGA-SESSION (6-10 juin 2026)

### Ce qui a été accompli

#### 1. Architecture d'instructions Claude — COMPLÈTE ✅
Mise en place d'un système d'instructions à 3 niveaux × 4 projets :

| Surface | Général | Cowork (global) | Cowork (projet) | Claude Code |
|---------|---------|-----------------|-----------------|-------------|
| Transverse | ✅ 8 blocs + sécurité | ✅ 10 blocs + sécurité conception | — | — |
| PhotoIQ | hérité | hérité | ✅ | ✅ CLAUDE.md + hooks + /ultrareview |
| TCC | hérité | hérité | ✅ | ✅ CLAUDE.md + hooks + /ultrareview |
| KazManager | hérité | hérité | ✅ (prompt ultime) | ⏳ CLAUDE.md protecteur à installer |
| Formation Skool | hérité | hérité | ✅ | ✅ CLAUDE.md |

**Instructions Général** (Réglages → Profil) : 8 sections — identité, rôle, communication, formats, fiabilité, garde-fous, sécurité réflexes permanents, hypothèses.

**Instructions Cowork** (Réglages → Cowork) : 10 blocs — identité, rôle, usages, manière de travailler, formats, qualité, fiabilité, autonomie (PAS DE CASSE + tests/TNR), sécurité fichiers, clarification. + Section "Sécurité dès la conception".

#### 2. Sécurité intégrée — DÉPLOYÉE ✅
Architecture de sécurité à 3 couches :
- **Comportemental** : instructions générales + CLAUDE.md par repo
- **Déterministe** : hooks guard.sh (bloque secrets + commandes destructrices)
- **Délibéré** : commande /ultrareview (gate GO/NO-GO avant prod)

Installé dans : PhotoIQ ✅, TCC ✅. À installer : KazManager (CLAUDE.md protecteur).

#### 3. PhotoIQ — RESTAURÉ ✅
- Nouveau projet Supabase créé (ref: sybfcbtugihbpotyuzxl, eu-west-1)
- Ancien projet supprimé (pausing free-tier > 90 jours)
- Variables Vercel mises à jour (DATABASE_URL, DIRECT_URL)
- Schema Prisma poussé (`npx prisma db push`)
- Keepalive cron installé (app/api/keep-alive/route.ts, schedule "0 8 */5 * *")
- Sécurité installée (CLAUDE.md + hooks + /ultrareview)
- URL : https://photoiq.vercel.app
- GitHub : samuelgomis/photoiq (main)
- ⚠️ Supabase free-tier : limite 2 projets actifs (photoiq + teranga-command-center)

#### 4. TCC — SÉCURISÉ ✅
- Middleware redirect : teranga-command-center.vercel.app → tcc-ai.sn (301)
- CLAUDE.md installé avec contexte complet (schémas, pipelines, doctrine)
- Sécurité installée (hooks + /ultrareview)
- URL prod : https://tcc-ai.sn
- GitHub : samuelgomis/teranga-command-center

#### 5. KazManager / n8n — MIGRÉ v2 ✅
- Migration n8n : v1.106.3 → v1.121.1 → v2.26.2
- 76 workflows intacts (48 actifs), 12 credentials intactes
- SSL/HSTS fonctionnel
- Architecture réseau découverte : nginx (host) → localhost:5678 → n8n_new
- n8n_new__bak (v1.117.3) arrêté mais conservé comme rollback
- Backups : /root/backup_n8n_pre_migration_20260610/ + SSD Lexar externe
- Docker-compose backups multiples sur le VPS
- URL : https://n8n.kazmanager.ai
- VPS : 145.223.34.126

**Rapport de migration v2** : 76/76 workflows compatibles, 7 instance issues (toutes config, 0 critical).

**Points à traiter plus tard** :
- Nettoyer N8N_RUNNERS_ENABLED=false du docker-compose (ignoré en v2)
- Nettoyer les 4 workflows en doublon (collisions webhook pré-existantes)
- Passer Task Runners de internal → external (n8nio/runners)
- Clarifier l'archi nginx → Traefik → n8n

#### 6. Formation Skool — STRUCTURÉE ✅
- Repo créé : ~/Desktop/formation-securite-claude/
- 18 fichiers : CLAUDE.md, README, calendrier, 5 templates, 6 scripts vidéo, 2 posts Skool
- Guides HTML : guide expert + tutoriel débutant
- Plan de formation : 5 modules (~2h), cible fondateurs no-code
- Pricing : 97€ standalone (early-bird 47€), upsell audit 297€
- Post communauté partagé dans QG IA Skool
- Premier retour reçu (demande tuto plus simple → validé)

---

## ÉTAT ACTUEL DES PROJETS

### PhotoIQ
- **Statut** : Beta, v1.4 sanctuarisée
- **Stack** : Next.js 14, TypeScript, Prisma, Supabase (sybfcbtugihbpotyuzxl), NextAuth v5, tRPC, PostHog, Claude API, ElevenLabs TTS
- **Déploiement** : Vercel (auto-deploy main)
- **Repo** : ~/Desktop/photoiq · github.com/samuelgomis/photoiq
- **Supabase** : free-tier, keepalive cron actif
- **Prochaines priorités** : retours beta Photo Club, itération UX, lancement public (photoiq.photography)

### TCC (Teranga Command Center)
- **Statut** : Production gouvernementale
- **Stack** : Next.js 15, Supabase (PostGIS + pgvector), Claude API (Haiku), n8n Cloud, Vercel
- **URL** : https://tcc-ai.sn
- **Repos** : ~/Desktop/Tourism-command-center (git) + ~/Desktop/@Tourism-command-center (dev)
- **Règle sync** : modifier @Tourism d'abord → copier vers Tourism → commit
- **Règle absolue** : TCC ne doit JAMAIS être pausé ou mis hors service

### KazManager
- **Statut** : GTM-Ready, CC V2 en cours
- **Stack** : Bubble.io (kazmanager.ai) + n8n v2.26.2 (VPS) + Redis 7
- **n8n** : https://n8n.kazmanager.ai — v2.26.2, 76 workflows, 48 actifs
- **VPS** : 145.223.34.126, containers : n8n_new (actif), kaz_redis_sentinel, n8n_new__bak (arrêté)
- **Archive** : /Users/test/Documents/#SAAS/AGENTS KAZMAN... (2 ans d'historique)
- **12 agents** : KazManager, Smart-Routing, KazSentinel V2 (Gates 1-10), KazVerifier, KazCoordinator, KazMemory, KazMetrics, KazPredictor, KazProspector, ReaderAgent, PromptReader, Configurator
- **Prochaines priorités** : CLAUDE.md protecteur archive, nettoyage workflows doublons, runner externe, migration Bubble → Supabase/Vercel

### Formation "Sécuriser Claude sans coder"
- **Statut** : Production contenu, semaine 1
- **Workspace** : ~/Desktop/formation-securite-claude/
- **Prochaine action** : poster module 0 gratuit dans Skool, sonder l'intérêt

---

## ACTIONS EN ATTENTE (priorité décroissante)

1. **KazManager — CLAUDE.md protecteur** : installer le CLAUDE.md dans le dossier archive (#SAAS/AGENTS KAZMAN...) avec règles de protection absolue (lecture seule, interdiction de suppression)
2. **KazManager — Nettoyage workflows** : désactiver/supprimer les 4 doublons stale qui causent des collisions webhook
3. **KazManager — Runner externe** : passer N8N_RUNNERS_MODE de internal à external + ajouter container n8nio/runners
4. **KazManager — Nettoyer docker-compose** : retirer N8N_RUNNERS_ENABLED=false (ignoré en v2), externaliser le mot de passe dans un .env
5. **KazManager — Migration Bubble → Supabase** : reconstruire CC V2 sur Vercel/Supabase (décision stratégique majeure)
6. **Formation Skool — Module 0** : poster le teasing, mesurer l'engagement
7. **PhotoIQ — Retours beta** : collecter et analyser les feedbacks Photo Club
8. **TCC — Archi réseau** : clarifier nginx → Traefik (double proxy)

---

## DÉCISIONS ARCHITECTURALES CLÉS PRISES

1. **Instructions 3 niveaux** : Général (transverse) → Cowork global (méthode de travail) → Projet (contexte spécifique). Jamais de contexte projet dans le global.
2. **Sécurité 3 couches** : Comportemental (instructions/CLAUDE.md) + Déterministe (hooks guard.sh) + Délibéré (/ultrareview). Le déterministe ne peut pas être contourné par le modèle.
3. **PAS DE CASSE** : toute modification est rétrocompatible, backup avant intervention, rollback documenté, TNR obligatoire.
4. **Workflow dual-instance** : Cowork planifie, Claude Code exécute. Cowork ne tape pas de commandes terminal. Code ne prend pas de décisions stratégiques.
5. **n8n : nginx → n8n_new** : le routage réel passe par nginx (host), pas par Traefik (Docker). Le docker-compose définit Traefik mais nginx prend la priorité sur les ports 80/443.

---

## FICHIERS ET EMPLACEMENTS CLÉS

| Fichier | Emplacement | Rôle |
|---------|-------------|------|
| Instructions Général | Réglages → Profil | Transverse chat + Cowork |
| Instructions Cowork | Réglages → Cowork → Instructions globales | 10 blocs + sécurité |
| Projet PhotoIQ | Cowork → Projects → photoiq | Contexte projet |
| Projet TCC | Cowork → Projects → TCC | Contexte projet |
| Projet KazManager | Cowork → Projects → KAZMANAGER | Prompt ultime |
| Projet Formation | Cowork → Projects → Formation Sécurité | Contexte formation |
| Backup n8n VPS | /root/backup_n8n_pre_migration_20260610/ | Workflows + credentials + volume |
| Backup n8n SSD | /Volumes/Lexar/backup_n8n_pre_migration_20260610/ | Copie externe |
| docker-compose actif | /root/docker-compose.yml (VPS) | Config Docker n8n + Traefik |
| docker-compose backup v2 | /root/docker-compose.yml.bak_pre_v2_20260610_115939 | Rollback v1.121.1 |
| Formation repo | ~/Desktop/formation-securite-claude/ | Workspace production cours |
| Guide expert HTML | formation-securite-claude/guides/securite-claude-guide.html | Pour la communauté |
| Tutoriel débutant HTML | formation-securite-claude/guides/securiser-claude-tutoriel.html | Pour la communauté |
| Plan formation HTML | formation-securite-claude/plan/formation-securite-claude-plan.html | Interne |

---

*Document généré le 10 juin 2026 — à charger en début de prochaine session Cowork.*
