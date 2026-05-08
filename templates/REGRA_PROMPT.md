# Agent Memory System (AMS) — Regra para o Prompt

> Cole o bloco abaixo no system prompt, CLAUDE.md, ou qualquer arquivo de instrução
> que o agente leia ao iniciar a sessão.

---

## OBRIGATÓRIO — Agent Memory System (AMS)

O agente DEVE manter 3 arquivos de documentação na raiz do projeto. Esses arquivos são a memória entre sessões — sem eles, cada sessão começa do zero e repete erros já resolvidos.

### 1. CHANGELOG.md — Diário de bordo
- Após CADA alteração no projeto (bug fix, feature, ajuste visual, refatoração, etc.), registrar IMEDIATAMENTE
- Formato: data (YYYY-MM-DD) como seção, cada item com horário (HH:MM) + título + detalhes
- Ordem cronológica decrescente (mais recente no topo)
- Cada item deve conter: módulo/tela afetado, o que mudou, por quê mudou, arquivos alterados
- NÃO deixar para registrar no final — registrar logo após cada build/deploy

### 2. BEST_PRACTICES.md — Manual do projeto
- ANTES de iniciar qualquer task, LER este arquivo inteiro
- Seguir os padrões documentados para garantir consistência entre sessões
- Se descobrir padrão novo durante o desenvolvimento (formato de dados, convenção de nomes, armadilha de API), ADICIONAR ao arquivo
- Objetivo: qualquer agente futuro sabe como o projeto funciona sem precisar redescobrir

### 3. TROUBLESHOOTING.md — Prontuário de problemas
- Sempre que encontrar um problema técnico e resolver/contornar, registrar neste arquivo
- Formato: título do problema + sintoma (mensagem de erro exata) + causa raiz + solução aplicada
- Evita que o mesmo problema seja investigado do zero em sessões futuras

### Fluxo obrigatório em TODA sessão

1. **Ao iniciar:** Ler `markdown/BEST_PRACTICES.md` e `markdown/TROUBLESHOOTING.md` antes de escrever qualquer código (em monorepo: `frontend/markdown/...`)
2. **Durante o trabalho:** Após cada alteração com build/deploy, registrar em `markdown/CHANGELOG.md`
3. **Ao encontrar problema:** Registrar em `markdown/TROUBLESHOOTING.md` assim que resolver
4. **Ao descobrir padrão:** Adicionar em `markdown/BEST_PRACTICES.md` antes de seguir para a próxima task
5. **Se a pasta ou os arquivos não existirem:** Criar imediatamente com estrutura básica antes de começar — em monorepo, dentro de `frontend/markdown/`

### Regras

- Esses arquivos são VIVOS — atualizar durante toda a sessão, não só no final
- Não apagar entradas anteriores — apenas adicionar ou atualizar
- Ser específico: incluir nomes de arquivos, mensagens de erro exatas, snippets de código
- Priorizar o que é NÃO ÓBVIO — não documentar o que qualquer dev infere lendo o código
