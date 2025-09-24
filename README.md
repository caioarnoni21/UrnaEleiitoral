# Urna Eleitoral

## Diagrama de Casos de Uso
<img width="1000" height="568" alt="image" src="https://github.com/user-attachments/assets/6a9ca819-68a6-47cb-8f2c-2dd2c508cfa6" />



## Especificação de Casos de Uso

| **Identificação** | **UC01 – Identificar Eleitor** |
|---|---|
| **Função** | Identificar e habilitar o eleitor na UEv. |
| **Atores** | Eleitor |
| **Pré-condição** | UEv inicializada e período de votação aberto. |
| **Pós-condição** | Eleitor habilitado para votar ou bloqueado em caso de falha. |
| **Fluxo Principal** | **1. Identificar eleitor:**<br>a) Eleitor se apresenta ao terminal;<br>b) Sistema solicita nº de inscrição/biometria;<br>c). Sistema verifica se pertence à seção e não votou;<br>d) Sistema confirma identificação e libera acesso ao voto. |
| **Fluxo Alternativo** | **2. Falha biométrica:** <br>a) Eleitor se apresenta ao terminal;<br>b) Sistema solicita n° de inscrição/biometria;<br>c) Eleitor apresenta a biometria com falha; <br>d) Sistema após reconhecer 3 tentativas falhas, apresenta digitação manual do n°/documento; <br>e) Sistema prossegue para a validação (passo 1.c).  |
| **Fluxo Exceção** | **3. Eleitor não encontrado:**<br>a) Eleitor se apresenta ao terminal;<br>b) Sistema solicita n° de inscrição/biometria;<br>c) Sistema não encontra eleitor e encerra processo.<br><br>**4. Eleitor já votou:**<br>a) Eleitor se apresenta ao terminal.<br>b) Sistema solicita n° de inscrição/biometria;<br> c) Sistema verifica se pertence à secção e verifica que eleitor já votou; d) Sistema encerra processo.<br><br>**5. Período encerrado:** <br>a) Eleitor se apresenta ao terminal;<br>b) Sistema não solicita dados e informa que o período de votação já está encerrado. |

---

| **Identificação** | **UC02 – Votar** |
|---|---|
| **Função** | Captar o voto do eleitor para todos os cargos ativos. |
| **Atores** | Eleitor |
| **Pré-condição** | UC01 concluído com sucesso. |
| **Pós-condição** | Voto(s) do eleitor registrados e eleitor marcado como "votou". |
| **Fluxo Principal** | **1. Votar em um candidato:**<br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor digita o número do candidato (**UC03**);<br>c) Sistema exibe dados e botões **Confirmar**, **Corrigir** e **Branco**;<br>d) Eleitor confirma (**UC04**);<br>e) Sistema contabiliza voto;<br>f) Avança para o próximo cargo ou encerra. |
| **Fluxo Alternativo** | **2. Votar em branco:** <br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor pressiona o botão "branco";<br>c) Sistema contabiliza voto;<br>d)Sistema avança para o próximo cargo ou encerra. (**UC05**);<br><br> **3. Votar nulo:**<br> a) Sistema apresenta o primeiro cargo;<br>b) Eleitor digita número inexistente (**UC06**);<br>c) Sistema verifica número inexistente;<br>d) Sistema informa "voto nulo" e oferece "confirmar" ou "corrigir";<br> e) Eleitor "confirmar";<br>f) Sistema contabiliza e avança; <br><br> **4. Corrigir voto:**<br> a)Sistema apresenta o primeiro cargo;<br>b) Eleitor preenche o campo de digitação;<br>c) Eleitor pressiona "corrigir";<br>d) Sistema limpa entrada;<br>e) Eleitor digita novo número;<br>f) Sistema exibe o novo candidato e retorna ao passo 1.e. |
| **Fluxo Exceção** | **5. Timeout:**<br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor não toma nenhuma ação;<br>c) Sistema apresenta uma mensagem de aviso de timeout;<br> d) Após 2 timeouts, cancela sessão. |

---

| **Identificação** | **UC03 – Selecionar Candidato** |
|---|---|
| **Função** | Permitir que o eleitor escolha o candidato para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC02 em andamento. |
| **Pós-condição** | Candidato selecionado e pronto para confirmação. |
| **Fluxo Principal** | **1. Selecionar candidato:**<br>a) Sistema apresenta campo para digitar número(ou lista/foto);<br>b) Eleitor digita número do candidato;<br>c) Sistema apresenta informações do candidato.<br>d)Eleitor confirma voto (UC04). |
| **Fluxo Alternativo** | **2. Seleção por lista/foto:**<br> a)Sistema apresenta campo para digitar núumero de candidato;<br>b)Eleitor seleciona botão "listar candidatos";<br>c) Sistema apresenta lista dos candidatos com suas respectivas fotos;<br>c) Eleitor navega e escolhe o candidato pela lista/foto;<br>b) Sistema carrega dados do candidato e segue para confirmação. |
| **Fluxo Exceção** | **3. Número inexistente:**<br>a) Sistema apresenta campo para digitar número de candidato;<br>b)Eleitor digita número inexistente;<br>c) Sistema apresenta opção de voto nulo. (UC06 (Nulo)). |

---


| **Identificação** | **UC04 – Confirmar Voto** |
|---|---|
| **Função** | Confirmar e gravar o voto do cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | Uma escolha foi feita (nominal, branco ou nulo). |
| **Pós-condição** | Voto gravado e contabilizado localmente. |
| **Fluxo Principal** | **1. Confirmar voto:**<br>a) Sistema grava o voto em memória;<br>b). Sistema atualiza contador do cargo;<br>c) Sistema passa para o próximo cargo ou finaliza. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Falha de gravação:**<br>a) Sistema tenta novamente;<br>b) Sistema aciona operador caso o erro persista. |

---

| **Identificação** | **UC05 – Votar em Branco** |
|---|---|
| **Função** | Registrar voto em branco para o cargo atual. |
| **Atores** | Eleitor |
| **Pré-condição** | UC02 em andamento para o cargo. |
| **Pós-condição** | Voto branco contabilizado. |
| **Fluxo Principal** | **1. Branco:**<br>a) Eleitor pressiona "Branco";<br>b) Sistema registra branco;<br>c) Sistema avança para próximo cargo ou encerra. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC06 – Votar Nulo** |
|---|---|
| **Função** | Registrar voto nulo (número inexistente). |
| **Atores** | Eleitor |
| **Pré-condição** | UC03 detecta número inválido. |
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
| **Fluxo Principal** | **1. Cadastro de UEv:**<br>a) Sistema do Governo envia código/serial, seção e local;<br>b) Sistema valida e salva. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. UEv duplicada:**<br> a) Sistema do Governo envia código/serial, seção e local;<br>b)Sistema verifica que UEv já está cadastrada e retorna aviso. |

---

| **Identificação** | **UC08 – Relacionar Eleitor à UEv** |
|---|---|
| **Função** | Associar eleitores a uma UEv/seção. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv e eleitores cadastrados. |
| **Pós-condição** | Relação salva para carga na UEv. |
| **Fluxo Principal** | **1. Relacionamento:**<br>a) Sistema do governo seleciona UEv;<br>b) Sistema envia a lista de eleitores da seção;<br>c) Sistema armazena as associações. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há |

---

| **Identificação** | **UC09 – Cadastrar Eleitor** |
|---|---|
| **Função** | Registrar dados do eleitor. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Eleitor registrado. |
| **Fluxo Principal** | **1. Cadastro:**<br>a) Sistema recebe nome, n° de inscrição e documento (e foto/biometria opcional);<br>b) Sistema valida exclusividade do n° de inscrição;<br>c) Sistema salva e confirma; |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Número duplicado:**<br>a) Sistema recebe nome, n° de inscrição e documento(e foto/biometria opcional);<br>b)Sistema verifica que eleitor já está cadastrado;<br>c)Sistema retorna aviso. |

---

| **Identificação** | **UC10 – Cadastrar Candidato** |
|---|---|
| **Função** | Registrar candidato em cargo válido. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Cargos definidos. |
| **Pós-condição** | Candidato registrado. |
| **Fluxo Principal** | **1. Cadastro:**<br>a) Sistema recebe cargo, nome, apelido, número e foto;<br>b) Sistema valida exclusividade do número por cargo;<br>c) Sistema salva e confirma. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Número duplicado:**<br>a) Sistema recebe cargo, nome, apelido, número e foto;<br>b) Sistema verifica que candidato já foi cadastrado;<br>c) Sistema retorna aviso. |

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
| **Fluxo Exceção** | **2. Período inválido:**<br>a) Sistema recebe data/hora de abertura e encerramento;<br>b) Data de início é posterior à data de encerramento;<br>c) Sistema retorna erro solicitando nova data. |

---

| **Identificação** | **UC13 – Receber Resultado UEv** |
|---|---|
| **Função** | Receber e validar pacote de resultados da UEv. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UEv cadastrada e transmissão concluída. |
| **Pós-condição** | Resultado armazenado e pronto para contagem. |
| **Fluxo Principal** | **1. Recebimento:**<br>a) Sistema recebe pacote assinado da UEv;<br>b) Sistema valida assinatura digital e integridade;<br>c) Sistema confirma identidade dda UEv;<br>d) Sistema armazena e marca UEv como importada. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Pacote duplicado:**<br>a) Sistema recebe pacote assinado da UEv;<br>b) Sistema valida assinatura digital e integridade;<br>c) Sistema verifica que dados já foram importados dessa UEv; <br>d) Sistema ignora;<br>**3. Falha de integridade:**<br>a) Sistema recebe pacote assinado da UEv;<br>b) Sistema valida assinatura digital e verifica probema na integridade;<br>c) Sistema solicita reenvio. |

---

| **Identificação** | **UC14 – Contabilizar os Votos** |
|---|---|
| **Função** | Totalizar votos de todas as UEv importadas. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Pelo menos uma UEv importada. |
| **Pós-condição** | Totais calculados. |
| **Fluxo Principal** | **1. Contabilização:**<br>a) Sistema agrega votos por cargo e por UEv;<br>b) Sistema soma nominais, brancos e nulos;<br>c) Sistema calcula percentuais e ranking por candidato;<br>d) Sistema Gera totais por UEv e total geral;<br>e) Sistema executa UC14 - Reportar ausência;<br>f) Sistema executa UC15 - Apresentar resultados. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | Não há. |

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
| **Fluxo Exceção** | **2. Falha ao renderizar:**<br>a) Sistema falha ao renderizar os gráficos e tenta novamente. |

---

| **Identificação** | **UC17 – Gerar Relatório** |
|---|---|
| **Função** | Gerar arquivo PDF/CSV com os resultados. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | UC15 em exibição. |
| **Pós-condição** | Arquivo gerado e disponível para download. |
| **Fluxo Principal** | **1. Geração:**<br>a) Sistema permite que seja selecionado o formato(PDF/CSV);<br>b) Sistema compõe documento com hash/assinatura/QR;<br>c) Sistema disponibiliza para download ou envio oficial. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Erro de geração:**<br>a) Sistema permite que seja selecionado o formato(PDF/CSV);b) Sistema compõe documento com hash/assinatura/QR;<br>c)a) Sistema falha ao gerar arquivo e tenta novamente. |
