# Urna Eleitoral

## Diagrama de Casos de Uso
<img width="1319" height="731" alt="Diagrama sem nome drawio" src="https://github.com/user-attachments/assets/82520a92-4ecc-4e62-a9f6-db997b44e057" />


## Especificação de Casos de Uso

| **Identificação** | **UC00 – Identificar Eleitor** |
|---|---|
| **Função** | Identificar e habilitar o eleitor na UEv. |
| **Atores** | Eleitor |
| **Pré-condição** | UEv inicializada e período de votação aberto. |
| **Pós-condição** | Eleitor habilitado para votar ou bloqueado em caso de falha. |
| **Fluxo Principal** | 1. Eleitor se apresenta ao terminal;<br>2. Sistema solicita nº de inscrição/biometria;<br>3. Sistema verifica se pertence à seção e não votou;<br>4. Sistema confirma identificação e libera acesso ao voto. |
| **Fluxo Alternativo** | **[FA01] Leitura por QR:** operador lê QR/código → ir ao passo 3;<br>**[FA02] Falha biométrica:** após 3 tentativas, permitir digitar nº/documento → passo 3. |
| **Fluxo Exceção** | **[FE01] Eleitor não encontrado:** encerra processo;<br>**[FE02] Eleitor já votou:** encerra processo;<br>**[FE03] Período encerrado:** bloqueia voto. |

---

| **Identificação** | **UC01 – Votar** |
|---|---|
| **Função** | Captar o voto do eleitor para todos os cargos ativos. |
| **Atores** | Eleitor |
| **Pré-condição** | UC00 concluído com sucesso. |
| **Pós-condição** | Voto(s) do eleitor registrados e eleitor marcado como "votou". |
| **Fluxo Principal** | 1. Sistema apresenta o primeiro cargo;<br>2. Eleitor digita o número do candidato (**UC02**);<br>3. Sistema exibe dados e botões **Confirmar**, **Corrigir** e **Branco**;<br>4. Eleitor confirma (**UC03**);<br>5. Sistema contabiliza voto;<br>6. Avança para o próximo cargo ou encerra. |
| **Fluxo Alternativo** | **[FA01] Branco:** eleitor pressiona Branco (**UC04**);<br>**[FA02] Nulo:** eleitor digita número inexistente (**UC05**);<br>**[FA03] Corrigir:** eleitor pressiona Corrigir e retorna ao passo 2. |
| **Fluxo Exceção** | **[FE01] Timeout:** reinicia tela; após 2 timeouts, cancela sessão;<br>**[FE02] Falha de hardware:** reinicia tela sem perder votos confirmados. |

---

| **Identificação** | **UC02 – Selecionar Candidato** |
|---|---|
| **Função** | Permitir que o eleitor escolha o candidato para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC01 em andamento. |
| **Pós-condição** | Candidato selecionado e pronto para confirmação. |
| **Fluxo Principal** | 1. Sistema apresenta campo para digitar número;<br>2. Eleitor digita número;<br>3. Sistema apresenta informações do candidato. |
| **Fluxo Alternativo** | **[FA01] Seleção por lista/foto:** eleitor seleciona na lista. |
| **Fluxo Exceção** | **[FE01] Número inexistente:** vai para UC05 (Nulo). |

---


| **Identificação** | **UC03 – Confirmar Voto** |
|---|---|
| **Função** | Confirmar e gravar o voto do cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | Uma escolha foi feita (nominal, branco ou nulo). |
| **Pós-condição** | Voto gravado e contabilizado localmente. |
| **Fluxo Principal** | 1. Sistema grava o voto em memória;<br>2. Atualiza contador do cargo;<br>3. Passa para o próximo cargo ou finaliza. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Falha de gravação:** tentar novamente ou acionar operador. |

---

| **Identificação** | **UC04 – Votar em Branco** |
|---|---|
| **Função** | Registrar voto em branco para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC01 em andamento para o cargo. |
| **Pós-condição** | Voto branco contabilizado. |
| **Fluxo Principal** | 1. Eleitor pressiona Branco;<br>2. Sistema registra branco;<br>3. Avança para próximo cargo ou encerra. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC05 – Votar Nulo** |
|---|---|
| **Função** | Registrar voto nulo (número inexistente). |
| **Atores** | Eleitor |
| **Pré-condição** | UC02 detecta número inválido. |
| **Pós-condição** | Voto nulo contabilizado. |
| **Fluxo Principal** | 1. Sistema informa número inválido;<br>2. Eleitor confirma ou corrige;<br>3. Se confirma → contabiliza nulo; se corrige → retorna à digitação. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC06 – Cadastrar UEv** |
|---|---|
| **Função** | Registrar urna eletrônica na UEg. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | UEv cadastrada e habilitada. |
| **Fluxo Principal** | 1. Administrador informa código/serial e seção;<br>2. Sistema valida e salva. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv duplicada:** rejeitar. |

---

| **Identificação** | **UC07 – Relacionar Eleitor à UEv** |
|---|---|
| **Função** | Associar eleitores a uma UEv/seção. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv e eleitores cadastrados. |
| **Pós-condição** | Relação salva para carga na UEv. |
| **Fluxo Principal** | 1. Selecionar UEv;<br>2. Associar lista de eleitores;<br>3. Salvar. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC08 – Cadastrar Eleitor** |
|---|---|
| **Função** | Registrar dados do eleitor. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Eleitor registrado. |
| **Fluxo Principal** | 1. Inserir dados do eleitor;<br>2. Validar unicidade;<br>3. Salvar. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Número duplicado:** rejeitar. |

---

| **Identificação** | **UC09 – Cadastrar Candidato** |
|---|---|
| **Função** | Registrar candidato em cargo válido. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Cargos definidos. |
| **Pós-condição** | Candidato registrado. |
| **Fluxo Principal** | 1. Inserir nome, número e foto;<br>2. Validar unicidade do número;<br>3. Salvar. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Número duplicado:** rejeitar. |

---

| **Identificação** | **UC10 – Definir Cargos** |
|---|---|
| **Função** | Criar e manter lista de cargos do pleito. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Lista de cargos criada/atualizada. |
| **Fluxo Principal** | 1. Administrador insere até 8 cargos;<br>2. Salva. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC11 – Definir Período de Votos** |
|---|---|
| **Função** | Definir data/hora de início e fim da votação. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Período de votação configurado. |
| **Fluxo Principal** | 1. Inserir datas de início/fim;<br>2. Salvar. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Tentativa de alterar após início:** rejeitar. |

---

| **Identificação** | **UC12 – Receber Resultado UEv** |
|---|---|
| **Função** | Receber e validar pacote de resultados da UEv. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv cadastrada e transmissão concluída. |
| **Pós-condição** | Resultado armazenado e pronto para contagem. |
| **Fluxo Principal** | 1. Receber pacote assinado;<br>2. Validar assinatura e integridade;<br>3. Armazenar e marcar como importado. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv não cadastrada:** rejeitar;<br>**[FE02] Pacote duplicado:** ignorar;<br>**[FE03] Falha de integridade:** solicitar reenvio. |

---

| **Identificação** | **UC13 – Contabilizar os Votos** |
|---|---|
| **Função** | Totalizar votos de todas as UEv importadas. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Pelo menos uma UEv importada. |
| **Pós-condição** | Totais calculados. |
| **Fluxo Principal** | 1. Somar votos nominais, brancos e nulos;<br>2. Calcular percentuais;<br>3. Chamar UC14 (Reportar Ausência);<br>4. Chamar UC15 (Apresentar Resultados). |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv ausente:** marcar apuração como parcial. |

---

| **Identificação** | **UC14 – Reportar Ausência** |
|---|---|
| **Função** | Listar eleitores que não votaram. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Contabilização concluída. |
| **Pós-condição** | Relatório de ausentes gerado. |
| **Fluxo Principal** | 1. Comparar lista de eleitores com votantes;<br>2. Gerar relatório de ausentes. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC15 – Apresentar Resultados** |
|---|---|
| **Função** | Exibir resultados em tabelas e gráficos. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UC13 finalizado. |
| **Pós-condição** | Resultados exibidos. |
| **Fluxo Principal** | 1. Exibir totais por cargo;<br>2. Oferecer opção de gerar relatório (UC16). |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Falha ao renderizar:** mostrar mensagem e permitir nova tentativa. |

---

| **Identificação** | **UC16 – Gerar Relatório** |
|---|---|
| **Função** | Gerar arquivo PDF/CSV com os resultados. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UC15 em exibição. |
| **Pós-condição** | Arquivo gerado e disponível para download. |
| **Fluxo Principal** | 1. Administrador escolhe formato;<br>2. Sistema gera arquivo com hash/assinatura. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Erro de geração:** exibir mensagem e permitir nova tentativa. |
