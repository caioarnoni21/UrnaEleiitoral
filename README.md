# Urna Eleitoral

## Diagrama de Casos de Uso
<img width="1319" height="731" alt="Diagrama sem nome drawio" src="https://github.com/user-attachments/assets/82520a92-4ecc-4e62-a9f6-db997b44e057" />


## Especificação de Casos de Uso

| **Identificação** | **UC01 – Identificar Eleitor** |
|---|---|
| **Função** | Identificar e habilitar o eleitor na UEv. |
| **Atores** | Eleitor |
| **Pré-condição** | UEv inicializada e período de votação aberto. |
| **Pós-condição** | Eleitor habilitado para votar ou bloqueado em caso de falha. |
| **Fluxo Principal** | **1. Identificar eleitor:**<br>a) Eleitor se apresenta ao terminal;<br>b) Sistema solicita nº de inscrição/biometria;<br>c). Sistema verifica se pertence à seção e não votou;<br>d) Sistema confirma identificação e libera acesso ao voto. |
| **Fluxo Alternativo** | **[FA01] Falha biométrica:** <br>a) Eleitor se apresenta ao terminal;<br>b) Sistema solicita biometria;<br>c) Eleitor apresenta a biometria com falha; <br>d) Sistema após reconhecer 3 tentativas falhas, apresenta digitação manual do n°/documento; <br>e) Sistema prossegue para a validação (passo 1.c).  |
| **Fluxo Exceção** | **[FE01] Eleitor não encontrado:** encerra processo;<br>**[FE02] Eleitor já votou:** encerra processo;<br>**[FE03] Período encerrado:** bloqueia voto. |

---

| **Identificação** | **UC02 – Votar** |
|---|---|
| **Função** | Captar o voto do eleitor para todos os cargos ativos. |
| **Atores** | Eleitor |
| **Pré-condição** | UC00 concluído com sucesso. |
| **Pós-condição** | Voto(s) do eleitor registrados e eleitor marcado como "votou". |
| **Fluxo Principal** | **1. Votar em um candidato:**<br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor digita o número do candidato (**UC02**);<br>c) Sistema exibe dados e botões **Confirmar**, **Corrigir** e **Branco ([FA03])**;<br>d) Eleitor confirma (**UC03**);<br>e) Sistema contabiliza voto;<br>f) Avança para o próximo cargo ou encerra. |
| **Fluxo Alternativo** | **2. [FA01] Votar em branco:** <br>a) Sistema apresenta campo para digitar;<br>b) Eleitor pressiona o botão "branco";<br>c) Sistema contabiliza voto;<br>d)Sistema avança para o próximo cargo ou encerra. (**UC04**);<br><br>3. **[FA02] Votar nulo:**<br> a) Sistema apresenta campo para digitar;<br>b) Eleitor digita número inexistente (**UC05**);<br>c) Sistema verifica número inexistente;<br>d) Sistema informa "voto nulo" e oferece "confirmar" ou "corrigir";<br> e) Eleitor "confirmar";<br>f) Sistema contabiliza e avança; <br><br> **4. [FA03] Corrigir voto:**<br> a) Eleitor pressiona "corrigir";<br>b)Sistema limpa entrada;<br>c) Eleitor digita novo número;<br>d) Sistema exibe o novo candidato e retorna ao passo 1.e. |
| **Fluxo Exceção** | **[FE01] Timeout:** reinicia tela; após 2 timeouts, cancela sessão;<br>**[FE02] Falha de hardware:** reinicia tela sem perder votos confirmados. |

---

| **Identificação** | **UC03 – Selecionar Candidato** |
|---|---|
| **Função** | Permitir que o eleitor escolha o candidato para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC01 em andamento. |
| **Pós-condição** | Candidato selecionado e pronto para confirmação. |
| **Fluxo Principal** | **1. Selecionar candidato:**<br>a) Sistema apresenta campo para digitar número(ou lista/foto);<br>b) Eleitor digita número do candidato;<br>c) Sistema apresenta informações do candidato.<br>d)Eleitor confirma voto (UC01). |
| **Fluxo Alternativo** | **[FA01] Seleção por lista/foto:**<br> a) Eleitor navega e escolhe o candidato pela lista/foto;<br>b) Sistema carrega dados do candidato e segue para confirmação. |
| **Fluxo Exceção** | **[FE01] Número inexistente:** vai para UC05 (Nulo). |

---


| **Identificação** | **UC04 – Confirmar Voto** |
|---|---|
| **Função** | Confirmar e gravar o voto do cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | Uma escolha foi feita (nominal, branco ou nulo). |
| **Pós-condição** | Voto gravado e contabilizado localmente. |
| **Fluxo Principal** | **1. Confirmar voto:**<br>a) Sistema grava o voto em memória;<br>b). Sistema atualiza contador do cargo;<br>c) Sistema passa para o próximo cargo ou finaliza. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Falha de gravação:**<br>a) Sistema tenta novamente;<br> Sistema aciona operador caso o erro persista. |

---

| **Identificação** | **UC05 – Votar em Branco** |
|---|---|
| **Função** | Registrar voto em branco para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC01 em andamento para o cargo. |
| **Pós-condição** | Voto branco contabilizado. |
| **Fluxo Principal** | **1. Branco:**<br>a) Eleitor pressiona "Branco";<br>b) Sistema registra branco;<br>c) Sistema avança para próximo cargo ou encerra. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC06 – Votar Nulo** |
|---|---|
| **Função** | Registrar voto nulo (número inexistente). |
| **Atores** | Eleitor |
| **Pré-condição** | UC02 detecta número inválido. |
| **Pós-condição** | Voto nulo contabilizado. |
| **Fluxo Principal** | **1. Nulo:**<br>a) Sistema informa número inválido;<br>b) Eleitor confirma;<br>c) Sistema contabiliza nulo. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC07 – Cadastrar UEv** |
|---|---|
| **Função** | Registrar urna eletrônica na UEg. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | UEv cadastrada e habilitada. |
| **Fluxo Principal** | **1. Cadastro de UEv:**<br>a) Sistema do Governoenvia código/serial, seção e local;<br>b) Sistema valida e salva. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv duplicada:** rejeitar. |

---

| **Identificação** | **UC08 – Relacionar Eleitor à UEv** |
|---|---|
| **Função** | Associar eleitores a uma UEv/seção. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv e eleitores cadastrados. |
| **Pós-condição** | Relação salva para carga na UEv. |
| **Fluxo Principal** | **1. Relacionamento:**a) Sistema do governo seleciona UEv;<br>b) Sistema envia a lista de eleitores da seção;<br>c) Sistema armazena as associações. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC09 – Cadastrar Eleitor** |
|---|---|
| **Função** | Registrar dados do eleitor. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Eleitor registrado. |
| **Fluxo Principal** | **1. Cadastro:**<br>a) Sistema recebe nome, n? de inscrição e documento (e foto/biometria opcional);<br>b) Sistema valida exclusividade do n? de inscrição;<br>c) Sistema salva e confirma; |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Número duplicado:** rejeitar. |

---

| **Identificação** | **UC10 – Cadastrar Candidato** |
|---|---|
| **Função** | Registrar candidato em cargo válido. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Cargos definidos. |
| **Pós-condição** | Candidato registrado. |
| **Fluxo Principal** | **1. Cadastro:**<br>a) Sistema recebe cargo, nome, apelido, número e foto;<br>b) Sistema valida exclusividade do número por cargo;<br>c) Sistema salva e confirma. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Número duplicado:** rejeitar. |

---

| **Identificação** | **UC11 – Definir Cargos** |
|---|---|
| **Função** | Criar e manter lista de cargos do pleito. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Lista de cargos criada/atualizada. |
| **Fluxo Principal** | **1. Definir cargos:**<br>a) Sistema recebe lista de cargos(máximo 8);<br>b) Sistema valida limites e salva; |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC12 – Definir Período de Votos** |
|---|---|
| **Função** | Definir data/hora de início e fim da votação. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Período de votação configurado. |
| **Fluxo Principal** | **1. Período:**<br>a) Sistema recebe data/hora de abertura e encerramento;<br>b) Sistema aplica configuração e registra auditoria. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Tentativa de alterar após início:** rejeitar. |

---

| **Identificação** | **UC13 – Receber Resultado UEv** |
|---|---|
| **Função** | Receber e validar pacote de resultados da UEv. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv cadastrada e transmissão concluída. |
| **Pós-condição** | Resultado armazenado e pronto para contagem. |
| **Fluxo Principal** | **1. Recebimento:**<br>a) Sistema recebe pacote assinado da UEv;<br>b) Sistema valida assinatura digital e integridade;<br>c) Sistema confirma identidade dda UEv;<br>d) Sistema armazena e marca UEv como importada. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv não cadastrada:** rejeitar;<br>**[FE02] Pacote duplicado:** ignorar;<br>**[FE03] Falha de integridade:** solicitar reenvio. |

---

| **Identificação** | **UC14 – Contabilizar os Votos** |
|---|---|
| **Função** | Totalizar votos de todas as UEv importadas. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Pelo menos uma UEv importada. |
| **Pós-condição** | Totais calculados. |
| **Fluxo Principal** | **1. Contabilização:**<br>a) Sistema agrega votos por cargo e por UEv;<br>b) Sistema soma nominais, brancos e nulos;<br>c) Sistema calcula percentuais e ranking por candidato;<br>d) Sistema Gera totais por UEv e total geral;<br>e) Sistema executa UC14 - Reportar ausência;<br>f) Sistema executa UC15 - Apresentar resultados. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] UEv ausente:** marcar apuração como parcial. |

---

| **Identificação** | **UC15 – Reportar Ausência** |
|---|---|
| **Função** | Listar eleitores que não votaram. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Contabilização concluída. |
| **Pós-condição** | Relatório de ausentes gerado. |
| **Fluxo Principal** | **1. Ausência:**<br>a) Sistema compara base de eleitores com a lista de votantes por UEv;<br>b) Sistema identifica ausentes por UEv;<br>c) Sistema gera listagem de ausentes. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC16 – Apresentar Resultados** |
|---|---|
| **Função** | Exibir resultados em tabelas e gráficos. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UC13 finalizado. |
| **Pós-condição** | Resultados exibidos. |
| **Fluxo Principal** | **1. Exibição:**<br>a) Sistema mostra totais por cargo (nominais, brancos, nulos, %);<br>b) Sistema permite filtragem por UEv; c) Sistema oferece opção UC16 - Gerar relatórios. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Falha ao renderizar:** mostrar mensagem e permitir nova tentativa. |

---

| **Identificação** | **UC17 – Gerar Relatório** |
|---|---|
| **Função** | Gerar arquivo PDF/CSV com os resultados. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UC15 em exibição. |
| **Pós-condição** | Arquivo gerado e disponível para download. |
| **Fluxo Principal** | **1. Geração:**<br>a) Sistema permite que seja selecionado o formato(PDF/CSV);<br>b) Sistema compõe documento com hash/assinatura/QR;<br>c) Sistema disponibiliza para download ou envio oficial. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **[FE01] Erro de geração:** exibir mensagem e permitir nova tentativa. |
