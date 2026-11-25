# Segundo Cérebro Unificado

Auditoria do ambiente e tutorial para Windows  
25 de novembro de 2026

## O que eu aproveitaria

**Começaria pelo Cérebro Unificado da worktree `d407` como base de execução.** Ele já tem memória pesquisável, decisões com fontes, fila, mensagens, MCP e um ateliê 3D ligado ao estado real. Colocaria o código em um repositório independente e o banco em uma pasta persistente fora de qualquer worktree. Usaria o Acervo de IA para localizar e selecionar fontes e o Obsidian para ler decisões e briefings em Markdown. Para telemetria, reaproveitaria o que o Segundo Cérebro original já sabe medir por cliente; para execução em outros provedores, usaria os adaptadores do Observatório como referência de desenho.

Essa escolha cobre três necessidades distintas. A memória compartilhada responde **o que já foi decidido**. A fila diz **quem vai fazer o quê e quando**. A CLI ou API de um provedor **executa a próxima chamada ao modelo**. Uma caixa de mensagens sozinha permite a entrega de contexto entre clientes já abertos. O worker é o componente que pode iniciar uma execução sem uma sessão humana ativa.

## 1. Inventário

| Componente | O que encontrei | Como usar |
|---|---|---|
| **Segundo Cérebro original** | Implementação na `2f18` e instalação em `%USERPROFILE%\.segundo-cerebro\app`. O vault `Documents\Segundo Cérebro` contém notas, projetos e turnos. O MCP recupera assunto, decisão vigente, justificativa, pendências e trechos originais. O painel local foi entregue na porta 8765 com filtros, tarefas, grafo e consumo de sessões observadas. | Fonte de decisões e referência para recuperação por turno e telemetria. |
| **Acervo de IA** | Dentro do vault, com `Catalogo.sqlite`, notas Markdown, coleções ZIP, grafo HTML e `Ferramentas\ponte.py`. O catálogo guarda origens e hashes. Nesta auditoria consultei coleções, notas e uma resposta histórica do Claude Code na caixa do Codex. O chat da entrega registra acesso também no Gemini CLI. | Importar fontes sob demanda e reutilizar a ideia de mensagem com ID de nota e `responder_a`. A caixa é persistente e o cliente a consulta durante uma sessão. |
| **Cérebro Unificado** | Código independente sob `d407\site 3d\cerebro-unificado`. Inclui SQLite/FTS5, captura com fila durável, aprovação com fonte, reserva de tarefa, worker, agendamento, MCP, importação e interface 3D. Os bancos de memória, fila de captura e operação têm responsabilidades próprias. A demo Aurora é fictícia e abre localmente na porta 8788. | Base recomendada para o projeto novo. O primeiro executor habilitável é Codex. As integrações de captura são uma capacidade separada da execução por modelo. |
| **Plano mestre** | Page de planejamento com roteiro modular, avaliação A/B, tecnologias candidatas e critérios de aceitação. Os arquivos de prompt e pesquisa, ambos na versão 2, detalham captura, privacidade, isolamento, workflows, grafo e ateliê. | Usar como roteiro para evoluir o código comprovado. Por exemplo, a versão da `d407` consulta deltas periodicamente. SSE aparece como opção de evolução. |
| **Observatório orbital** | API local Python/SQLite na porta 8776 e modo offline com estado no navegador. Chat com debate e síntese, seleção de modelos e adaptadores para Codex CLI, Claude CLI, Ollama, APIs compatíveis e Anthropic. | Referência concreta de roteamento, sessões e interface. O histórico de debate vira contexto adicional por participante, então o modo de conselho faz sentido para decisões específicas. |
| **Carbon** | `Desktop\Carbon` tem notas Dataview, inventário de agentes, modelos, conectores, orquestradores e conversor de Markdown para dados do dashboard. As métricas de exemplo estão escritas na nota. | Reaproveitar a forma de catalogar capacidades. Alimentar o painel novo com eventos observados por execução. |
| **Nexus Brain** | ZIP de exportação do AI Studio com README, metadados e configuração de build. A listagem do pacote inspecionado não contém o código de entrada da interface ou um executor de modelo. | Referência de conceito. A existência de um pool real ou de uma aplicação executável continua sem demonstração no ZIP. |
| **Claude-Mem, GSD e Antigravity** | Há instalação/catalogação de ferramentas e subagentes, incluindo 66 definições na coleção de subagentes Codex de 18/11. Um chat de 21/11 registrou falha de autenticação do observador do Claude-Mem. O Acervo tem documentos do Antigravity e um snapshot de `blissful-bell\fix_theme_and_ui`. A worktree do Antigravity existe no disco, está no commit `4b5788d` e tem uma aplicação Vite com `src/`. | Usar GSD para escolher papéis específicos e avaliar Claude-Mem como fonte opcional quando o observador estiver saudável. Tratar Antigravity e Gemini CLI como conectores distintos. |
| **Obsidian Vault** | A pasta com esse nome em Documents apresentou apenas a configuração do Obsidian no escopo da inspeção. O conteúdo de memória encontrado estava no vault **Segundo Cérebro**. | Abrir diretamente o vault que contém `Início.md` e `Acervo de IA`. |

Fontes centrais. [Prompt atualizado](https://chatgpt.com/library?file_id=libfile_613d5f1f776c8191a5f7c928f1d85fb2&account_id=personal) · [Mapa de pesquisa atualizado](https://chatgpt.com/library?file_id=libfile_c49ab412ea7881918381583b30ed96f0&account_id=personal) · [Plano mestre](https://chatgpt.com/space/page_96bf88d4c54c81918d34359b96e829da)

### Worktrees do Site 3D

O Git lista o checkout principal em `Documents\ChatGPT\site 3d`, mais **17 worktrees vinculadas**, das quais 14 estão na área de worktrees do Codex. O inventário de estado abaixo é um retrato da leitura. Em `b275`, `2f18` e `d407` os arquivos centrais que motivam esta auditoria aparecem como **não rastreados** pelo checkout pai.

| Worktree | HEAD e conteúdo observado |
|---|---|
| `b275` | `80d7684`, destacado. `PROMPT-segundo-cerebro.md` contém a especificação original. |
| `2f18` | `80d7684`, destacado. `segundo_cerebro/` e `tests/` contêm o primeiro app, adaptadores, dashboard e telemetria. |
| `d407` | `3c5e497`, destacado. `cerebro-unificado/`, pacote portátil, testes, documentação e capturas. A mesma worktree contém alterações do Observatório. |
| `3195`, `87b1`, `febe` | `3c5e497`, destacados. Variações com mudanças no Observatório. `3195` também traz `Habblaud-analise/`. |
| `0e3b`, `5a82` | `80d7684`, destacados, sem alterações reportadas pelo Git. O Acervo tem snapshots anteriores associados ao Observatório. |
| `1426`, `37f4`, `6ece` | `80d7684`, destacados. Ambiente Codex e arquivos locais de dependências. Há `outputs/` na `1426`. |
| `444e`, `cd42` | `80d7684`, destacados, com mudança de configuração de ambiente Codex. |
| `skills-guia` | `b486c58` em `codex/skills-guia`, sem alterações reportadas. Manual e auditorias de ferramentas, com módulos de arquitetura, qualidade e automação. |
| `orbital-cena`, `orbital-interface`, `orbital-servidor` | Worktrees em `Documents\ChatGPT`, com branches `codex/orbital-cena`, `codex/orbital-interface` e `codex/orbital-servidor`. Registram o trabalho paralelo do Observatório: cena e player offline (`2fd5e46`), busca e ficha de vértices (`8b11471`) e servidor com adaptadores e testes (`af6ec86`). A cena tem mudanças locais adicionais. |

**A consequência para a continuidade é direta.** Um commit identificado como `3c5e497` é só a base Git da `d407`. Um novo checkout naquele commit sozinho deixa de fora `cerebro-unificado/`. Para preservar essa entrega, use o ZIP validado, ou confira e faça uma cópia seletiva da pasta, antes de qualquer limpeza da worktree. Mantenha a nota de tarefa vinculada ao caminho da worktree, à branch e ao commit. [Git worktree](https://git-scm.com/docs/git-worktree) · [Worktrees do Codex](https://learn.chatgpt.com/docs/environments/git-worktrees)

### O que os chats acrescentaram

| Fonte | Decisão ou evidência |
|---|---|
| **Criar prompt para cérebro universal**, Codex, 10/11, `01a1c373-7878-7e71-b6a4-49c64dd8cf62` | O teste desejado era começar no Codex e dizer apenas “continue de onde paramos” em um Claude limpo. O `b275` registra continuidade, fontes literais e correção de decisões entre clientes. |
| **Criar segundo cérebro compartilhado**, Codex, 10/11, `01a1c37c-18b6-7110-ba88-33e3c24638ef` | O teste documentado recuperou o detalhe literal a partir de `Turno-32e2f3e8a2bc1726cc2ff034` e refletiu a mudança da escolha de pulseira para cartão, com fonte em `Turno-5fae4b4585879eb0f79df87b`. O chat também pediu consumo de tokens por modelo e provedor. |
| **Organizar cérebro compartilhado de IAs**, Codex, 18/11, `01a1eda6-0df0-7160-99ea-8f1b437dcbbb` | O foco foi catálogo de arquivos e comunicação direta entre clientes. A caixa consultada agora retornou a mensagem 2 do Claude Code em resposta à mensagem 1 do Codex. |
| **Pesquisa sobre memória unificada**, ChatGPT, 20–21/11 | A arquitetura pede memória por projeto, dados fictícios para demonstração e ateliê 3D em pixel art. Você especificou que o projeto é independente do GapTutor e pediu uma sessão Astra 6.2 Ultra ligada ao Site 3D. |
| **Implementar Cérebro Unificado**, Codex, 21/11, `01a2001c-0dc0-78d1-9d49-14b871a5f8fb` | O registro local confirma que a sessão usou a `d407`. A entrega documenta o fluxo Aurora, revisão com SHA-256, conciliação de thread do Codex e testes dos conectores com respostas de teste. |
| **Consumo do Codex**, ChatGPT, 22/11 | Você relatou aumento no percentual de 5 h/semanal com Astra 6.2 High e levantou a hipótese de que a ausência do cérebro antigo gerava mais repetição. Também pediu garantia de que o contexto enxuto preserve qualidade. Ainda falta medição comparável para atribuir a causa. |
| **Arquitetura do Segundo Cérebro**, ChatGPT, 24/11 | Organizou o plano mestre com fases, limites de cobertura e avaliação da economia. A Page declara que é planejamento. A worktree anterior fornece evidência separada da implementação. |

Também li as mensagens pertinentes da sessão do Observatório. Ela documenta a ideia de agentes em worktrees separadas, dois coordenadores e debate entre modelos. Para o seu piloto, use um coordenador e uma revisão independente quando a tarefa justificar. A comparação entre dois coordenadores pode ser um experimento com custo, duração e divergências registrados.

### Resultado da auditoria

- **Versão original `2f18`.** Reexecutei os **15 testes** numa cópia isolada. Na primeira tentativa, o caminho temporário padrão do ambiente tinha caracteres recusados pelo gerador de hooks. Com o diretório temporário da auditoria, os 15 passaram.
- **Cérebro Unificado `d407`.** Reexecutei os **sete testes de captura**, que passaram. Os outros 12 encontraram uma recusa do ambiente Windows ao criar o hard link inicial de identidade (`os.link`, WinError 5). Na mesma cópia, o comando `demo-mcp` passou em separado: três clientes, uma tarefa, uma tentativa e estado `delivered`. O ZIP passou na verificação de integridade, com 59 entradas. O relatório histórico documenta 19 testes aprovados e Playwright. O histórico também distingue as sondas de cliente com provedor sintético em loopback de uma chamada com conta de nuvem.
- **Escopo.** Examinei o Git, arquivos, código, registros selecionados do Codex, conversas recuperadas do ChatGPT e as duas fontes atualizadas. As conclusões sobre Git e testes se referem aos checkouts observados. Sessões privadas de outros clientes, disponibilidade atual de cada conta, cobertura integral de chats e consumo real da assinatura ficaram fora do que pude confirmar.


## 2. Monte uma instalação nova no Windows

### Passo 1 — Separe código, dados e notas

Use o pacote portátil para começar com o código do ateliê. Ele está dentro de `d407` e a raiz do ZIP já contém os arquivos da aplicação. Os comandos criam uma pasta nova, interrompem a extração se a pasta de código já existir e deixam os arquivos de memória fora da árvore de Git.

```powershell
$source = Join-Path $env:USERPROFILE '.codex\worktrees\d407\site 3d\cerebro-unificado'
$zip = Join-Path $source '.build\cerebro-unificado.zip'
$homeBrain = Join-Path $env:USERPROFILE 'Documents\CerebroPiloto'
$repoBrain = Join-Path $homeBrain 'codigo'
$dataBrain = Join-Path $homeBrain 'dados'
$vaultBrain = Join-Path $homeBrain 'notas'

if (-not (Test-Path -LiteralPath $zip)) { throw 'ZIP do Cérebro Unificado ausente.' }
if (Test-Path -LiteralPath $repoBrain) { throw 'A pasta codigo já existe. Escolha outro destino.' }

New-Item -ItemType Directory -Path $repoBrain,$dataBrain,$vaultBrain | Out-Null
Expand-Archive -LiteralPath $zip -DestinationPath $repoBrain

Set-Location -LiteralPath $repoBrain
git init -b main
git status --short --untracked-files=all
# Após conferir os arquivos do pacote:
git add .
git diff --cached --stat
git commit -m "Importa base local do Cérebro Unificado"
```

Abra `notas` como pasta no Obsidian. Comece com `Início.md` e `Projetos\piloto\BRIEF.md`. A aplicação funciona com o Obsidian fechado. Use o banco do Cérebro Unificado como fonte de autoridade para o estado operacional e publique no vault somente decisões, procedimentos, evidências e briefings que você queira consultar. Nesta versão, trate a publicação como manual até implementar um exportador incremental. Uma edição humana no Markdown pode se tornar proposta com o ID e a revisão de origem. [Como o Obsidian armazena arquivos](https://help.obsidian.md/Files+and+folders/How+Obsidian+stores+data)

### Passo 2 — Prove a operação local com o Aurora

Em um PowerShell normal na pasta `codigo`, use Python 3.11+ e Git. O script da aplicação cria a venv e instala os requisitos na primeira execução. O comando abaixo usa a política de execução existente no PowerShell. Se o Windows bloquear o script, inspecione o arquivo e use o comando por processo descrito no README do projeto.

```powershell
Set-Location -LiteralPath $repoBrain
.\Iniciar.ps1
```

No ateliê, abra **Aurora → Íris → Revisar Prova cromática Aurora**. Abra a decisão, a mensagem humana e o grafo. Execute a verificação e confira a evidência SHA-256, a entrega e o replay. Em outro terminal na pasta do projeto:

```powershell
$brainPy = (Resolve-Path -LiteralPath '.\.venv\Scripts\python.exe').Path
& $brainPy -X utf8 -m unittest discover -s tests
& $brainPy -X utf8 -m brain.cli demo-mcp
```

O ensaio MCP usa um banco temporário. O resultado esperado tem três clientes, uma tarefa, uma tentativa e `delivered`. Se os testes do Aurora derem Windows Error 5 ao criar `demo-identities.json`, repita no PowerShell normal com pasta local NTFS que permita hard links. A captura pode ser validada isoladamente com `-p test_capture.py`.

### Passo 3 — Crie um projeto piloto com escopo próprio

1. Copie `examples\projeto.json` para `CerebroPiloto\projeto.json`. Dê ao projeto um ID estável, como `piloto`. No arquivo, use uma identidade humana, um agente por cliente quando precisar atribuir trabalho, e uma identidade de conector por origem que você habilitar. O campo `token_env` contém o nome de uma variável, o valor fica fora do JSON, Git e Obsidian.
2. Disponibilize valores independentes de credencial aos processos que precisam deles. Para o exemplo incluído, os nomes são `CEREBRO_CURADOR`, `CEREBRO_REVISOR` e `CEREBRO_CAPTURA`. Configure no Windows ou na sessão que vai iniciar cada cliente. Comece com `capture: []` enquanto valida a passagem de contexto manualmente.
3. Na pasta do app, inicialize o projeto. As variáveis `$dataBrain` e `$homeBrain` são as do Passo 1. Ajuste o ID passado a `-Projeto` ao ID que gravou no JSON.

```powershell
$projectConfig = Join-Path $homeBrain 'projeto.json'
& $brainPy -m brain.cli --data $dataBrain --config $projectConfig init-project
.\Iniciar.ps1 -Dados $dataBrain -Config $projectConfig -Projeto piloto -Porta 8790
```

O primeiro dado útil deve ser uma decisão curta com justificativa e fonte. Grave também uma proposta de agente, uma tarefa aberta, um critério objetivo e um detalhe que fique só no material original. Assim você consegue testar retomada e busca de evidência em separado.

### Passo 4 — Ligue Codex, Claude Code e Gemini CLI ao mesmo projeto

Cada cliente deve iniciar o **mesmo** servidor MCP stdio com o Python da venv, pasta de trabalho do código ou `PYTHONPATH` equivalente, banco compartilhado, projeto explícito e credencial da sua identidade. No seu arquivo de projeto, cadastre as identidades antes de configurar os clientes. Para todos os processos, o executável é `C:\...\codigo\.venv\Scripts\python.exe`. Os argumentos têm esta forma:

```text
-m brain.mcp_server --data C:\caminho\CerebroPiloto\dados --project piloto --token-env CEREBRO_REVISOR
```

| Cliente | Onde configurar e verificar |
|---|---|
| Codex | Uma entrada local em `.codex/config.toml` ou configuração escolhida no cliente. Configure `command`, `args`, `cwd` e repasse a variável de identidade ao subprocesso. Confira com `codex mcp list` e consulte uma nota piloto no chat do projeto. |
| Claude Code | MCP stdio com escopo local do projeto. Informe executável e argumentos e garanta `PYTHONPATH` da pasta de código para o processo do servidor. Confira com `claude mcp list` ou `/mcp`. Configure outro `token_env` no projeto para essa identidade. |
| Gemini CLI | `mcpServers` no `.gemini/settings.json` do piloto, com `command`, `args` e `cwd`. Confira com `gemini mcp list` ou `/mcp`. Use a terceira identidade. |

Exemplo para Codex no Windows. Caminhos TOML com aspas simples preservam as barras invertidas. Adapte os caminhos e deixe a variável indicada disponível ao Codex antes de abrir o projeto.

```toml
[mcp_servers.cerebro_piloto]
command = 'C:\caminho\CerebroPiloto\codigo\.venv\Scripts\python.exe'
cwd = 'C:\caminho\CerebroPiloto\codigo'
args = ['-m', 'brain.mcp_server', '--data', 'C:\caminho\CerebroPiloto\dados', '--project', 'piloto', '--token-env', 'CEREBRO_REVISOR']
env_vars = ['CEREBRO_REVISOR']
```

Teste sem partir para a captura automática. No Codex, registre uma proposta via `contribute` e envie uma mensagem via `send` ao agente Gemini ou Claude usando a chave estável `piloto-revisao-01`. No outro cliente, consulte `inbox`, abra o registro com `get` e responda com `reply`. Depois faça essa sessão recuperar a decisão e a justificativa via `resume` e o detalhe original via `search`/`get`. Para confirmar o isolamento, configure um segundo projeto de teste e tente achar a mesma frase com esse outro projeto ativo. [MCP no Codex](https://learn.chatgpt.com/docs/extend/mcp) · [MCP no Claude Code](https://code.claude.com/docs/en/mcp) · [MCP no Gemini CLI](https://geminicli.com/docs/tools/mcp-server/)

### Passo 5 — Capture só o necessário

Depois da prova anterior, siga `docs\CAPTURA.md`. Copie `examples\capture.local.example.json` para uma pasta privada e defina projeto, raiz, dados e credenciais. Adicione um conector por vez, mesclando os exemplos `codex.hooks.json`, `claude.hooks.json` e `gemini.hooks.json` com a configuração existente. O processo que drena a fila recebe a mesma configuração e credencial do conector.

```powershell
$captureConfig = Join-Path $homeBrain 'captura.json'
& $brainPy -m brain.capture --config $captureConfig --origin codex drain
```

Teste primeiro prompt, segundo turno, retomada, interrupção, fork e duplicata. Comece com um projeto de teste e verifique o que os hooks de cada cliente realmente entregaram. Use a conciliação do Codex App Server para uma thread conhecida e autorizada quando a captura mostrar lacuna. Para chats comuns do ChatGPT, o caminho reproduzível é a exportação oficial com importação pré-visualizada. A abertura passiva de chat no Desktop e o Antigravity merecem testes próprios. [Hooks do Codex](https://learn.chatgpt.com/docs/hooks) · [Claude Code](https://code.claude.com/docs/en/hooks) · [Gemini CLI](https://geminicli.com/docs/hooks/reference/) · [Exportação do ChatGPT](https://help.openai.com/en/articles/7260999-exporting-your-chatgpt-history-and-data)

## 3. Crie projetos e orquestre agentes

### A tarefa é a unidade de trabalho

O coordenador cria um briefing com objetivo, critérios, arquivos relevantes, decisão vigente, restrições, referências de fonte, commit-base e teste. Cada contribuição volta com resultado, evidência, comandos executados, incertezas e próximos passos. Use a mesma nota em qualquer provedor. Em cada projeto, o `AGENTS.md` pode começar assim:

```markdown
# Regras do projeto
- Preserve os critérios da tarefa e as decisões vigentes citadas no briefing.
- Para retomar, consulte o MCP do projeto ou abra Projetos/piloto/BRIEF.md.
- Se faltar contexto, procure o trecho e abra a fonte antes de supor.
- Rode os testes da área alterada. Amplie quando o risco ou a mudança exigir.
- Registre alterações, teste, resultado e fontes no fim da tarefa.
```

No Claude Code e Gemini CLI, use suas instruções de projeto equivalentes e mantenha o briefing como ponteiro compartilhado. Um procedimento longo fica no acervo, com consulta sob demanda. Use o mesmo objetivo em todos os clientes e envie a cada especialista apenas o material da sua função. [AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) · [Contexto do Gemini CLI](https://geminicli.com/docs/cli/gemini-md/)

### Um workflow para repetir

1. **Planejar.** O coordenador lê o briefing, define critérios e registra as dependências. Para trabalho pequeno, ele mesmo implementa e valida.
2. **Delegar.** Se houver frentes independentes, envie cada tarefa com saída verificável. Exemplo: um implementador escreve o parser e testes na worktree de implementação. Um pesquisador examina documentação e entrega evidências em leitura. Um revisor lê o diff depois que a implementação está pronta.
3. **Reservar.** Use `assign`, `claim` e `renew` no MCP. A identidade que reserva recebe um `attempt_id`. Conclusão usa `complete` com esse ID, validação e fonte. Se a reserva expirar, uma tentativa anterior perde autoridade para concluir.
4. **Integrar.** O implementador entrega commit e resumo do diff. O coordenador revisa contra os critérios, integra por commit e roda os testes no checkout de integração. Uma decisão de produto que surgir no processo é proposta até você aprová-la.
5. **Registrar.** Publique um resultado curto, vincule o commit, atualize as pendências e arquive a worktree depois de verificar que a entrega está preservada. [Subagentes no Codex](https://learn.chatgpt.com/docs/agent-configuration/subagents) · [Git worktree](https://git-scm.com/docs/git-worktree)

```powershell
# Na raiz de um projeto Git, após um commit base revisado.
$baseCommit = git rev-parse --verify HEAD
git worktree add -b task/piloto-parser ..\piloto-parser $baseCommit
git worktree add -b task/piloto-validacao ..\piloto-validacao $baseCommit
git worktree list --porcelain
```

Dê aos dois agentes escopos de escrita distintos. Quando a revisão depende do patch, passe o commit da implementação e use leitura ou um checkout próprio para testar esse commit. Use subagentes nativos quando o coordenador e os especialistas estiverem no mesmo runtime. Use a fila/MCP entre runtimes, com um teto de concorrência para cada projeto e interrupção quando o trabalho exceder o orçamento definido. Começaria com um executor e um revisor, com revisão adicional sob demanda para arquitetura, decisões caras ou divergências reais.

### Automatize o primeiro fluxo completo

A demo implementa **artefato disponível → tarefa de revisão → mensagem → reserva → resultado com evidência**. Na pasta do projeto, estes comandos atuam sobre a demo padrão quando nenhuma configuração de projeto é passada. Use os IDs e as chaves da demo para experimentos.

```powershell
& $brainPy -m brain.cli rule status
& $brainPy -m brain.cli artifact --key piloto-prova-01
& $brainPy -m brain.cli worker once
& $brainPy -m brain.cli schedule once
```

Ao reproduzir o evento, conserve a mesma chave e verifique uma única tarefa lógica. Ao automatizar um relatório diário, grave o checkpoint depois de salvar a contribuição de resumo e reutilize a identidade da janela pendente em caso de interrupção. O README documenta `schedule enable`, `pause`, `worker enable` e o Agendador do Windows para `once`. Versões futuras podem publicar artefatos de CI ou receber webhooks. Faça a troca para serviços distribuídos quando a fila local deixar de atender a duração ou concorrência exigida.


## 4. Faça chamadas diretas a outros modelos

Há duas rotas. **CLIs** usam o perfil que você autenticou no cliente e podem acessar ferramentas e a worktree conforme a política local. **APIs** usam credenciais, modelos e cobrança da plataforma e são convenientes para tarefas de texto com contrato controlado. O aplicativo, CLI e API podem listar modelos diferentes mesmo quando pertencem ao mesmo provedor.

| Rota | Conexão | Evidência de saída |
|---|---|---|
| Codex CLI | `codex exec --json --sandbox read-only` com texto via stdin | JSONL. Evento `turn.completed` com uso quando disponível. |
| Claude Code | `claude -p --output-format json --permission-mode plan` | JSON de resultado. Use com um checkout e ferramentas adequados ao escopo. |
| Gemini CLI | Prompt via stdin em modo headless, com `--output-format json` | JSON de resposta e estatísticas por modelo. |
| OpenAI API | `POST https://api.openai.com/v1/responses`, Bearer `OPENAI_API_KEY` | `output` e `usage`. |
| Anthropic API | `POST https://api.anthropic.com/v1/messages`, `x-api-key` e `anthropic-version` | `content`, `usage` e indicação de término. |
| Gemini API | `POST https://generativelanguage.googleapis.com/v1beta/models/{model}:generateContent`, `x-goog-api-key` | `candidates` e `usageMetadata`. |

Documentação. [Codex não interativo](https://learn.chatgpt.com/docs/non-interactive-mode) · [Claude Code programático](https://code.claude.com/docs/en/headless) · [Gemini CLI headless](https://geminicli.com/docs/cli/headless/) · [OpenAI Responses](https://developers.openai.com/api/reference/resources/responses/methods/create/) · [Anthropic Messages](https://platform.claude.com/docs/en/api/messages/create) · [Gemini generateContent](https://ai.google.dev/api/generate-content)

Em PowerShell 7, execute cada linha isoladamente no repositório conforme o provedor que deseja testar. Cada comando pode consumir a cota do cliente. Configure o modelo pelo perfil local ou pela opção da CLI. O prompt sintético pede só uma resposta de texto.

```powershell
$brief = 'Responda apenas com o texto: conexao-piloto-ok'
$brief | codex exec --json --sandbox read-only -
$brief | claude -p --output-format json --permission-mode plan
$brief | gemini --output-format json
```

A `d407` já sabe chamar o Codex quando `codex_executable` está configurado e o executor `codex-exec` é escolhido. O modo com `codex_panel_profile` usa App Server para retomar a mesma thread do painel. O Observatório tem a referência para adicionar Claude CLI, Ollama e provedores via API. Mantenha o contrato do worker da `d407` e acrescente um adaptador por provedor, com um projeto sintético de teste para cada um.

### Uma chamada via API

O exemplo usa o Gemini. Disponibilize `GEMINI_API_KEY` ao processo e selecione em `CEREBRO_GEMINI_MODEL` um ID disponível na sua conta, sem o prefixo `models/`. Abra os endpoints de Responses ou Messages na tabela para substituir autenticação, corpo e parser no adaptador correspondente.

```powershell
$model = $env:CEREBRO_GEMINI_MODEL
if (-not $model -or -not $env:GEMINI_API_KEY) {
    throw 'Configure CEREBRO_GEMINI_MODEL e GEMINI_API_KEY no processo.'
}
$brief = 'Responda apenas com o texto: conexao-piloto-ok'
$body = @{
    contents = @(@{ role = 'user'; parts = @(@{ text = $brief }) })
    generationConfig = @{ maxOutputTokens = 256 }
} | ConvertTo-Json -Depth 8 -Compress
$request = @{
    Method = 'Post'
    Uri = "https://generativelanguage.googleapis.com/v1beta/models/$($model):generateContent"
    Headers = @{ 'x-goog-api-key' = $env:GEMINI_API_KEY }
    ContentType = 'application/json'
    Body = $body
    TimeoutSec = 60
}
$answer = Invoke-RestMethod @request
$answer.candidates[0].content.parts | ForEach-Object { $_.text }
$answer.usageMetadata
```

Em produção, o adaptador recebe `{task_id, attempt_id, provider, model, briefing, budget}` e devolve `{status, output, source_refs, usage, request_id, duration_ms}`. Grave a intenção antes de enviar a chamada. Em caso de timeout após envio, marque efeito incerto e concilie antes de repetir. Defina fallback por tarefa e pelo escopo de dados que o outro provedor pode receber. Cada chamada segue a autenticação e a cota do seu provedor. Os exemplos de nuvem são para reprodução no seu perfil e não foram chamados nesta auditoria.

## 5. Economize contexto sem sacrificar qualidade

1. **Retome com recuperação progressiva.** Comece com decisões, pendências e referências. No MCP da `d407`, experimente `resume(budget=6000)`, onde `budget` está em **caracteres**. Faça `search(limit=5)` e abra as fontes necessárias por `get`. Leia a evidência inteira quando a ambiguidade ou a gravidade justificar.
2. **Prepare a entrada localmente.** Use Git, busca textual, lint e scripts de teste para filtrar. Forneça a faixa relevante do diff, a falha e os caminhos. Carregue anexos, skills e MCPs ligados ao escopo atual. Escreva uma nota de continuidade após decisão ou conclusão de tarefa. Hooks podem copiar e indexar registros sem chamar um modelo para resumir todo turno.
3. **Escolha esforço por risco.** Fixe Astra 6.2 High no primeiro A/B para medir o efeito da memória isoladamente. Em uma rodada posterior, teste esforço menor para inventário e mudanças mecânicas. Preserve o nível de raciocínio de tarefas difíceis até a rubrica mostrar que um ajuste mantém a qualidade.
4. **Delegue só trabalho que renda em paralelo.** Um especialista recebe a pergunta e as fontes do seu papel. A resposta volta com evidência e resumo. Em tarefas simples, usar uma sessão evita repetir briefing, ferramentas e revisão.
5. **Use os dois tipos de cache com métricas próprias.** O cache local guarda resultados de busca por projeto, consulta e revisão. Em APIs com cache de prompt, mantenha instruções estáveis no prefixo e insira o material variável depois. Registre os tokens em cache e confira o recurso no modelo e endpoint. O texto continua ocupando janela de contexto. [Orientações de uso do Work e Codex](https://learn.chatgpt.com/docs/pricing) · [Cache de prompt](https://developers.openai.com/api/docs/guides/prompt-caching) · [Limites de uso](https://help.openai.com/en/articles/20001625-understanding-chatgpt-and-codex-usage-limits)

### Como medir no Astra 6.2

Faça primeiro **cinco pares** de tarefas, depois amplie para vinte se o processo de medição estiver consistente. Inclua retomada, criação de projeto, implementação, correção de bug e revisão. Prepare a mesma base e os mesmos testes em cada par. Alterne a ordem, use sessões limpas e mantenha modelo e esforço fixos. Registre cache e atividade concorrente.

| Observe em cada execução | Como comparar |
|---|---|
| Requisitos, testes, regressões e retrabalho | Use rubrica comum e avaliação cega quando possível. Conserve os mesmos critérios em ambas as condições. |
| Tokens de entrada, saída, cache e raciocínio | Registre o que cada cliente expõe. Marque ausências como desconhecidas. Cache e raciocínio podem já estar incluídos em totais do provedor. |
| Tempo, falhas, chamadas e execuções de subagentes | Some todos os agentes envolvidos no mesmo resultado aceito. |
| Percentual das janelas de 5 h e semanal | Anote imediatamente antes e depois, com horário, resets, modelo e sessões concorrentes. Se a janela reiniciar, invalide aquela comparação de percentual. |

**A** usa seu fluxo habitual. **B** usa o mesmo fluxo com briefing curto e recuperação sob demanda. Calcule a economia mediana dos pares válidos, por exemplo `1 − tokens_B / tokens_A`. Use como hipótese uma redução de 30% no contexto inicial, com aprovação dos mesmos critérios de qualidade. Registre a diferença de cota em coluna própria. O relato de 22/11 estabelece a hipótese. A relação causal com a remoção do cérebro antigo ainda precisa de dados. [Gerenciamento do uso do Astra](https://help.openai.com/en/articles/20001516-managing-usage-with-gpt-6-astra-in-work-and-codex)

### Use o dashboard para tomar decisões

A **fila** mostra o que está bloqueado e quem tem a reserva. O **grafo** leva de uma decisão ao turno e ao artefato que a sustentam. A **telemetria** mostra por tarefa o modelo solicitado, o modelo e provedor informados, a rota, tokens, latência e lacunas. A cena 3D deve abrir a mesma ficha que a lista. Use eventos do mesmo banco para alimentar a cena, o replay e os gráficos.

Para telemetria, modele `run_id`, `attempt_id`, `project_id`, `client`, `provider_reported`, `model_reported`, `input_tokens`, `cached_input_tokens`, `output_tokens`, `reasoning_tokens`, `duration_ms` e `coverage`. Quando um gateway só expõe um alias, registre o alias e o que está desconhecido. Use `2f18` como referência e confira as semânticas por provedor antes de somar.

## 6. Roteiro para construir o núcleo em outro repositório

| Etapa | Implemente | Prova de que terminou |
|---|---|---|
| 1. Memória | SQLite em WAL com projeto, fontes, decisões, mensagens e tarefas. FTS5, busca por projeto e consulta por ID. Markdown projeta o estado no vault. | Uma decisão vigente e uma substituída voltam com fonte. A busca de outro projeto preserva o escopo. |
| 2. MCP | `resume` com orçamento, `search` paginado, `get`, caixa e contribuição atribuída. Derive projeto e ator da credencial. | Dois clientes recuperam o mesmo assunto e um detalhe fora do resumo. |
| 3. Execução | Fila SQL, chave de idempotência, reserva atômica, prazo de lease e `attempt_id`. Comece com verificador determinístico e depois ligue uma CLI/API. | Reentrega preserva uma tarefa. Reserva expirada rejeita a conclusão antiga. |
| 4. Captura e exportação | Adaptadores versionados com fila durável, indicador de cobertura, exportação incremental por ID e revisão. | Interromper e retomar preserva os turnos disponíveis. Reimportar mantém a contagem. |
| 5. Painel e escala | Snapshot, deltas e lista primeiro. Grafo e 3D operam sobre a mesma projeção. Meça recuperação antes de adicionar embeddings ou filas externas. | A cena e a lista mostram a mesma ficha. O replay preserva a revisão selecionada. |

**Comece com esta prova.** Em um projeto fictício, escolha uma opção no Codex e anote uma palavra imprevisível. Retome em outro cliente, recupere a decisão e localize a palavra pelo turno. Corrija a decisão no segundo cliente e volte ao primeiro para verificá-la. Dispare duas vezes o mesmo artefato e confirme uma tarefa, uma tentativa e uma evidência. Por fim, faça cinco pares de testes de consumo. Isso valida memória, orquestração, integração e a hipótese de economia no seu fluxo.

