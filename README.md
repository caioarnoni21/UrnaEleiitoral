# Urna Eleitoral

## Diagrama de Casos de Uso
<img width="1197" height="676" alt="image" src="https://github.com/user-attachments/assets/465e4877-65f8-4754-b2df-33b7376edaa6" />




## Especificação de Casos de Uso

| **Identificação** | **UC01 – Votar** |
|---|---|
| **Função** | Captar o voto do eleitor para todos os cargos ativos. |
| **Atores** | Eleitor |
| **Pré-condição** | Eleitor com identificação válida e período de votações aberto. |
| **Pós-condição** | Voto(s) do eleitor registrados e eleitor marcado como "votou". |
| **Fluxo Principal** | **1. Votar em um candidato:**<br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor digita o número do candidato;<br>c) Sistema exibe dados e botões **Confirmar**, **Corrigir** e **Branco**;<br>d) Eleitor confirma ;<br>e) Sistema contabiliza voto;<br>f) Avança para o próximo cargo ou encerra. |
| **Fluxo Alternativo** | **2. Votar em branco:** <br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor pressiona o botão "branco";<br>c) Sistema contabiliza voto;<br>d)Sistema avança para o próximo cargo ou encerra.<br><br> **3. Votar nulo:**<br> a) Sistema apresenta o primeiro cargo;<br>b) Eleitor digita número inexistente;<br>c) Sistema verifica número inexistente;<br>d) Sistema informa "voto nulo" e oferece "confirmar" ou "corrigir";<br> e) Eleitor "confirmar";<br>f) Sistema contabiliza e avança; <br><br> **4. Corrigir voto:**<br> a)Sistema apresenta o primeiro cargo;<br>b) Eleitor preenche o campo de digitação;<br>c) Eleitor pressiona "corrigir";<br>d) Sistema limpa entrada;<br>e) Eleitor digita novo número;<br>f) Sistema exibe o novo candidato e retorna ao passo 1.e. |
| **Fluxo Exceção** | **5. Timeout:**<br>a) Sistema apresenta o primeiro cargo;<br>b) Eleitor não toma nenhuma ação;<br>c) Sistema apresenta uma mensagem de aviso de timeout;<br> d) Após 2 timeouts, cancela sessão. |

---

| **Identificação** | **UC02 – Gerenciar eleição** |
|---|---|
| **Função** | Criar, validar, iniciar e encerrar a eleição. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Eleição criada, validada, iniciada ou encerrada. |
| **Fluxo Principal** | **1.Criação da eleição:**<br>a) Sistema inicia criação da eleição;<br>b) Sistema valida a relação de cargos e candidatos;<br>c) Sistema valida as UEvs; <br>d) Sistema solicita período de eleição(início e fim); |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Candidatos/Cargos inválidos:**<br> a) Sistema inicia criação da eleição;<br>b)Sistema quantidade inválida de cargos(0) ou candidatos(0 ou 1).<br> **3. UEv duplicada:**<br>a) Sistema inicia criação da eleição;<br>b) Sistema valida a relação de cargos e candidatos;<br>c) Sistema detecta duplicidade de UEv e solicita manutenção;<br>**4. Período inválido:**<br>a) Sistema inicia criação da eleição;<br>b) Sistema valida a relação de cargos e candidatos;<br>c) Sistema valida as UEvs; <br>d) Sistema solicita período de eleição(início e fim);<br>e) Sistema verifica data inválida(data inicial < data atual ou data final > data inicial). |

---

| **Identificação** | **UC03 – Gerenciar candidatos** |
|---|---|
| **Função** | Gerenciar os candidatos e seus respecitvos cargos. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Cargos e candidatos prontos para serem associados à eleição. |
| **Fluxo Principal** | **1. Gerenciar candidatos :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Criar novo cargo";<br>c) Sistema solicita e valida cargo(quantidade de cargos criados, número e nome).<br>d)Sistema exibe opção de "Cadastrar candidato" e "Gerenciar candidato";<br>e) Administrador seleciona "Cadastrar candidato";<br>f)Sistema solicita dados do candidato(nome, apelido, número e fotografia).<br>g) Sistema valida e salva candidato.|
| **Fluxo Alternativo** |  **2. Excluir cargo :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Editar cargo";<br>c) Sistema soclita nome do cargo;<br>d) Sistema apresenta candidatos do cargo, opção "Editar candidato" e "Editar cargo"<br>e)Administrador seleciona "Editar cargo";<br>f) Sistema apresenta os campos do nome e número do cargo editáveis e opções "Salvar" e "Excluir"<br> g) Administrador seleciona "Excluir"<br>h) Sistema exclui cargo e seus candidatos.|<br><br>
**3. Excluir candidato :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Editar cargo";<br>c) Sistema soclita nome do cargo;<br>d) Sistema apresenta candidatos do cargo, opção "Editar candidato" e "Editar cargo"<br>e)Administrador seleciona "Editar candidato";<br>f) Sistema apresenta lista dos canidatos à esse cargo;<br> g) Administrador seleciona candidato a ser editado;<br>h)Sistema apresenta dados do candidto(nome, apelido, número e fotografia) editáveis e opções "Salvar" e "Excluir"<br> g) Administrador seleciona "Excluir"<br>h) Sistema exclui candidato selecionado.|<br><br>
(editar)
| **Fluxo Exceção** | **4. Número máximo de cargos :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Criar novo cargo";<br>c) Sistema verifica quantidade limite de cargos cadastrados(8) e exibe lista de edição de cargos. |

---

| **Identificação** | **UC04 – Contabilizar votos** |
|---|---|
| **Função** | Registrar dados do eleitor. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Administrador autenticado. |
| **Pós-condição** | Eleitor registrado. |
| **Fluxo Principal** | **1. Cadastro:**<br>a) Sistema recebe nome, n° de inscrição e documento (e foto/biometria opcional);<br>b) Sistema valida exclusividade do n° de inscrição;<br>c) Sistema salva e confirma; |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Número duplicado:**<br>a) Sistema recebe nome, n° de inscrição e documento(e foto/biometria opcional);<br>b)Sistema verifica que eleitor já está cadastrado;<br>c)Sistema retorna aviso. |

---

| **Identificação** | **UC05 – Disponibilizar resultados** |
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
