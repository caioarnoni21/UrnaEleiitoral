# Urna Eleitoral

# Especificação de Casos de Uso


| **Identificação**|**UC00 – Identificar Eleitor** |
|---|---|
| **Função** | Identificar e habilitar o eleitor na UEv. |
| **Atores** | Eleitor. |
| **Pré-condição** | UEv inicializada e período de votação aberto. |
| **Pós-condição** | Eleitor habilitado para votar ou bloqueado em caso de falha. |
| **Fluxo principal** | 1. Eleitor se apresenta ao terminal;<br>2. Sistema solicita nº de inscrição/biometria;<br>3. Sistema verifica se pertence à seção e não votou;<br>4. Sistema confirma identificação e libera acesso ao voto. |
| **Fluxo alternativo** | **[FA01] Leitura por QR:** operador lê QR/código → ir ao passo 3;<br>**[FA02] Falha biométrica:** após 3 tentativas, permitir digitar nº/documento → passo 3. |
| **Fluxo exceção** | **[FE01] Eleitor não encontrado** → encerrar;<br>**[FE02] Eleitor já votou** → encerrar;<br>**[FE03] Período encerrado** → encerrar. |

---

| **Identificação**|**UC01 – Votar** |
|---|---|
| **Função** | Captar o voto do eleitor para todos os cargos ativos. |
| **Atores** | Eleitor. |
| **Pré-condição** | UC00 concluído com sucesso. |
| **Pós-condição** | Voto(s) do eleitor registrados e eleitor marcado como "votou". |
| **Fluxo principal** | 1. Sistema apresenta o primeiro cargo;<br>2. Eleitor digita o número do candidato (**UC02**);<br>3. Sistema exibe os dados e botões **Confirmar**, **Corrigir** e **Branco**;<br>4. Eleitor confirma (**UC03**);<br>5. Sistema contabiliza voto;<br>6. Avança para o próximo cargo ou encerra. |
| **Fluxo alternativo** | **[FA01] Branco:** eleitor pressiona Branco (**UC04**).<br>**[FA02] Nulo:** eleitor digita número inexistente (**UC05**).<br>**[FA03] Corrigir:** eleitor pressiona Corrigir e retorna ao passo 2. |
| **Fluxo exceção** | **[FE01] Timeout:** reinicia tela; após 2 timeouts, cancela sessão.<br>**[FE02] Falha de hardware:** reinicia tela sem perder votos confirmados. |

---

| **Identificação**|**UC02 – Selecionar Candidato** |
|---|---|
| **Função** | Permitir que o eleitor escolha o candidato para o cargo atual. |
| **Atores** | Eleitor. |
| **Pré-condição** | UC01 em andamento. |
| **Pós-condição** | Candidato selecionado e pronto para confirmação. |
| **Fluxo principal** | 1. Sistema apresenta campo para digitar número;<br>2. Eleitor digita número;<br>3. Sistema apresenta informações do candidato. |
| **Fluxo alternativo** | **[FA01] Seleção por lista/foto:** eleitor seleciona na lista. |
| **Fluxo exceção** | **[FE01] Número inexistente:** vai para UC05 (Nulo). |

---

### UC03 – Confirmar Voto

| **Identificação**|**UC02 – Selecionar Candidato** |
|---|---|
| **Função** | Confirmar e gravar o voto do cargo atual. |
| **Atores** | Eleitor. |
| **Pré-condição** | Uma escolha foi feita (nominal, branco ou nulo). |
| **Pós-condição** | Voto gravado e contabilizado localmente. |
| **Fluxo principal** | 1. Sistema grava o voto em memória;<br>2. Atualiza contador do cargo;<br>3. Passa para o próximo cargo ou finaliza. |
| **Fluxo exceção** | **[FE01] Falha de gravação:** tentar novamente ou acionar operador. |

---

### UC04 – Votar em Branco

| **Campo** | **Descrição** |
|---|---|
| **Função** | Registrar voto em branco para o cargo atual. |
| **Atores** | Eleitor. |
| **Fluxo principal** | 1. Eleitor pressiona Branco;<br>2. Sistema registra branco e contabiliza;<br>3. Avança para próximo cargo ou encerra. |

---

### UC05 – Votar Nulo

| **Campo** | **Descrição** |
|---|---|
| **Função** | Registrar voto nulo (número inexistente). |
| **Atores** | Eleitor. |
| **Fluxo principal** | 1. Sistema informa que o número é inválido;<br>2. Eleitor confirma nulo ou corrige;<br>3. Se confirmar → contabiliza nulo; se corrigir → retorna à digitação. |

---

### UC06 – Cadastrar UEv

| **Campo** | **Descrição** |
|---|---|
| **Função** | Registrar urna eletrônica na UEg. |
| **Atores** | Administrador. |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | UEv cadastrada e habilitada. |
| **Fluxo principal** | 1. Administrador informa identificação da UEv (código/serial, seção);<br>2. Sistema valida e salva. |
| **Fluxo exceção** | **[FE01] UEv duplicada:** rejeitar. |

---

### UC07 – Relacionar Eleitor à UEv

| **Campo** | **Descrição** |
|---|---|
| **Função** | Vincular eleitores a uma seção/UEv específica. |
| **Atores** | Administrador. |
| **Pré-condição** | Eleitores e UEv cadastrados. |
| **Pós-condição** | Relação salva para carga na UEv. |
| **Fluxo principal** | 1. Selecionar seção/UEv;<br>2. Associar eleitores;<br>3. Salvar. |

---

### UC08 – Cadastrar Eleitor

| **Campo** | **Descrição** |
|---|---|
| **Função** | Registrar eleitor na base de dados. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Inserir nome, nº inscrição, documento;<br>2. Validar unicidade e salvar. |
| **Fluxo exceção** | **[FE01] Número duplicado:** rejeitar cadastro. |

---

### UC09 – Cadastrar Candidato

| **Campo** | **Descrição** |
|---|---|
| **Função** | Cadastrar candidato para um cargo. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Inserir cargo, nome, número e foto;<br>2. Validar número único;<br>3. Salvar. |
| **Fluxo exceção** | **[FE01] Número duplicado:** rejeitar. |

---

### UC10 – Definir Cargos

| **Campo** | **Descrição** |
|---|---|
| **Função** | Criar e manter a lista de cargos do pleito. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Inserir nome dos cargos (até 8);<br>2. Salvar configuração. |

---

### UC11 – Definir Período de Votos

| **Campo** | **Descrição** |
|---|---|
| **Função** | Definir data/hora de início e fim da votação. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Selecionar datas e horários;<br>2. Salvar configuração. |
| **Fluxo exceção** | **[FE01] Tentativa de alterar após início:** bloquear. |

---

### UC12 – Receber Resultado UEv

| **Campo** | **Descrição** |
|---|---|
| **Função** | Receber e validar pacote de resultados da UEv. |
| **Atores** | Administrador, Sistema do Governo. |
| **Fluxo principal** | 1. Receber pacote assinado;<br>2. Validar integridade e identidade;<br>3. Armazenar e marcar como importado. |
| **Fluxo exceção** | **[FE01] UEv não cadastrada:** rejeitar;<br>**[FE02] Pacote duplicado:** ignorar;<br>**[FE03] Falha de integridade:** solicitar reenvio. |

---

### UC13 – Contabilizar os Votos

| **Campo** | **Descrição** |
|---|---|
| **Função** | Totalizar votos de todas as UEv importadas. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Somar votos nominais, brancos e nulos;<br>2. Calcular percentuais;<br>3. Chamar UC14 (Reportar Ausência);<br>4. Chamar UC15 (Apresentar Resultados). |
| **Fluxo exceção** | **[FE01] UEv ausente:** marcar apuração parcial. |

---

### UC14 – Reportar Ausência

| **Campo** | **Descrição** |
|---|---|
| **Função** | Listar eleitores que não votaram. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Sistema cruza base de eleitores com lista de votantes;<br>2. Gera relatório de ausentes. |

---

### UC15 – Apresentar Resultados

| **Campo** | **Descrição** |
|---|---|
| **Função** | Mostrar os resultados em tabelas/gráficos. |
| **Atores** | Administrador, Sistema do Governo. |
| **Fluxo principal** | 1. Exibir totais por cargo (nominais, brancos, nulos);<br>2. Disponibilizar opção de exportar (UC16). |

---

### UC16 – Gerar Relatório

| **Campo** | **Descrição** |
|---|---|
| **Função** | Gerar arquivo PDF/CSV dos resultados. |
| **Atores** | Administrador. |
| **Fluxo principal** | 1. Administrador escolhe formato;<br>2. Sistema gera arquivo com hash/assinatura. |
| **Fluxo exceção** | **[FE01] Erro na geração:** notificar e permitir nova tentativa. |

