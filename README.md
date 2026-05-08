# Agent Memory System (AMS)

*A memória que faz o agente evoluir a cada sessão.*

---

## O que é

Um sistema de **3 arquivos + 1 regra** que transforma cada sessão de IA em aprendizado cumulativo. O agente nunca repete o mesmo erro, nunca redescobre o que já sabe, e entrega cada vez mais rápido.

## O problema

Toda sessão de IA começa **do zero**:

- Mesmos bugs investigados de novo, toda vez
- Padrões redescobertos a cada sessão
- Decisões tomadas sem saber o que já foi decidido
- Tempo desperdiçado refazendo trabalho que já existe

## A solução

3 arquivos vivos numa pasta `markdown/` dentro do projeto que o agente **lê antes de codar** e **atualiza após cada entrega**:


| Arquivo | Função | Analogia |
|---------|--------|----------|
| `BEST_PRACTICES.md` | Como as coisas funcionam aqui | Manual do projeto |
| `TROUBLESHOOTING.md` | O que já deu errado e como resolveu | Prontuário médico |
| `CHANGELOG.md` | O que já foi feito e quando | Diário de bordo |

### Onde colocar a pasta `markdown/`

| Tipo de projeto | Local da pasta |
|---|---|
| Monorepo com frontend e backend separados (ex: `frontend/`, `backend/`) | `frontend/markdown/` |
| Projeto único (sem subpasta de frontend) | `markdown/` na raiz |

> **Padrão:** quando existe pasta `frontend/`, a memória mora dentro dela — fica perto do código que mais muda e versionada junto com o app entregue ao usuário. Em projeto único, a pasta vai na raiz.

## O ciclo virtuoso

```
Sessão 1: Agente descobre padrão → registra no BEST_PRACTICES
Sessão 2: Agente lê antes de codar → já sabe o padrão → entrega mais rápido
Sessão 2: Agente encontra bug → resolve → registra no TROUBLESHOOTING
Sessão 3: Mesmo bug aparece → agente lê → resolve em segundos
...
Sessão N: Agente é praticamente um dev sênior do projeto
```

## Por que funciona

- **Não depende de memória do modelo** — funciona com qualquer IA, qualquer sessão, qualquer provider
- **Portável** — troca de agente ou modelo e o conhecimento permanece
- **Auditável** — qualquer humano lê e entende o histórico completo
- **Cumulativo** — cada sessão deixa o projeto mais inteligente
- **Zero infraestrutura** — são arquivos markdown, versionados com o projeto
- **Colaborativo** — múltiplos agentes e desenvolvedores contribuem para a mesma base

## Como aplicar

### Passo 1 — Criar a pasta `markdown/` e copiar os templates

Crie a pasta `markdown/` dentro do projeto e copie os 3 arquivos da pasta `templates/` para dentro dela:

\`\`\`
# Monorepo (com frontend/ separado)
templates/CHANGELOG.md        →  seu-projeto/frontend/markdown/CHANGELOG.md
templates/BEST_PRACTICES.md   →  seu-projeto/frontend/markdown/BEST_PRACTICES.md
templates/TROUBLESHOOTING.md  →  seu-projeto/frontend/markdown/TROUBLESHOOTING.md

# Projeto único (sem frontend/)
templates/CHANGELOG.md        →  seu-projeto/markdown/CHANGELOG.md
templates/BEST_PRACTICES.md   →  seu-projeto/markdown/BEST_PRACTICES.md
templates/TROUBLESHOOTING.md  →  seu-projeto/markdown/TROUBLESHOOTING.md
\`\`\`

### Passo 2 — Adicionar a regra no prompt do agente

Copie o conteúdo de `templates/REGRA_PROMPT.md` e cole no **system prompt**, **CLAUDE.md**, ou qualquer arquivo de instrução que o agente leia ao iniciar.

### Passo 3 — Pronto

A partir da primeira tarefa, o agente começa a construir a memória do projeto automaticamente.

## Estrutura dos templates

```
agent-memory-system/
├── README.md                          ← Este arquivo
└── templates/
    ├── CHANGELOG.md                   ← Template do diário de bordo
    ├── BEST_PRACTICES.md              ← Template do manual do projeto
    ├── TROUBLESHOOTING.md             ← Template do prontuário
    └── REGRA_PROMPT.md                ← Regra para colar no prompt do agente
```

## Dicas de uso

1. **Versione os arquivos** — commite junto com o código. O histórico do git mostra a evolução do conhecimento
2. **Revise periodicamente** — remova entradas obsoletas, consolide padrões que mudaram
3. **Incentive contribuição humana** — devs humanos também podem (e devem) adicionar entradas
4. **Um AMS por projeto** — cada projeto tem seu contexto. Não compartilhe entre projetos diferentes
5. **Não economize no TROUBLESHOOTING** — quanto mais detalhado o sintoma e a solução, mais tempo economiza no futuro

## Compatibilidade

Testado e funciona com:
- Claude (Opus, Sonnet, Haiku) via Claude Code, API, ou qualquer harness
- Qualquer agente que aceite system prompt customizado
- Projetos de qualquer stack (React, Node, Python, Go, etc.)

O AMS não depende de nenhuma feature específica de IA — são apenas arquivos de texto que o agente é instruído a ler e manter.

---

*Criado por Felipe — Plataforma Mitra*
