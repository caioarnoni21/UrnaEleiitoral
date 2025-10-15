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
| **Fluxo Alternativo** |  **2. Excluir cargo :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Editar cargo";<br>c) Sistema soclita nome do cargo;<br>d) Sistema apresenta candidatos do cargo, opção "Editar candidato" e "Editar cargo"<br>e)Administrador seleciona "Editar cargo";<br>f) Sistema apresenta os campos do nome e número do cargo editáveis e opções "Salvar" e "Excluir"<br> g) Administrador seleciona "Excluir"<br>h) Sistema exclui cargo e seus candidatos.<br><br>**3. Excluir candidato :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Editar cargo";<br>c) Sistema soclita nome do cargo;<br>d) Sistema apresenta candidatos do cargo, opção "Editar candidato" e "Editar cargo"<br>e)Administrador seleciona "Editar candidato";<br>f) Sistema apresenta lista dos canidatos à esse cargo;<br> g) Administrador seleciona candidato a ser editado;<br>h)Sistema apresenta dados do candidto(nome, apelido, número e fotografia) editáveis e opções "Salvar" e "Excluir"<br> g) Administrador seleciona "Excluir"<br>h) Sistema exclui candidato selecionado.|<br><br>
(editar)
| **Fluxo Exceção** | **4. Número máximo de cargos :**<br>a) Sistema exibe lista de cargos e opção para "Criar novo cargo" e "Editar cargo";<br>b) Administrador seleciona "Criar novo cargo";<br>c) Sistema verifica quantidade limite de cargos cadastrados(8) e exibe lista de edição de cargos. |

---

| **Identificação** | **UC04 – Contabilizar votos** |
|---|---|
| **Função** | Receber, validar e contabilizar os votos por cada UEv(100máx.). |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Eleição finalizada e todos votos recebidos. |
| **Pós-condição** | Votos apurados por canditado, variações de votos(ausentes, brancos e nulos) e por UEv. |
| **Fluxo Principal** | **1. Disponibilizar total de votos:**<br>a) Sistema valida se eleição já concluiu o período de votação;<br>b) Sistema recebe dados validados das UEvs;<br>c) Sistema organiza dados por UEvs, cargos, candidatos, votos brancos e nulos;<br>d) Sistema notifica eleitores ausentes.|
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Período de eleição incompleto:**<br>a) Sistema verifica que a "data atual < data de finalização da eleição" e retorna notificação . | |

---

| **Identificação** | **UC05 – Disponibilizar resultados** |
|---|---|
| **Função** | Apresentar resultados da eleição. |
| **Atores** | Sistema do Governo |
| **Pré-condição** | Votos validados(UC04). |
| **Pós-condição** | Relatórios da eleição em forma de tabela ou gráficos, apresentados de maneira geral ou separados por UEv. Incluindo votos brancos, nulos e eleitores ausentes. |
| **Fluxo Principal** | **1. Gerar relatórios:**<br>a) Sistema valida dados recebidos;<br>b) Sistema organiza dados de forma geral e separados por UEv;<br>c) Sistema apresenta esses dados em forma de gráficos e tabelas.d) Sistema disponibiliza dados para download. |
| **Fluxo Alternativo** | Não há |
| **Fluxo Exceção** | **2. Ausência de dados:**<br>a) Sistema não recebe dados para gerar os relatórios. |


# Diagrama de Sequencia 

## UC 01 - VOTAR

<img width="320" height="624" alt="image" src="https://github.com/user-attachments/assets/93b7ad8a-9500-4a22-817a-5dfe80e57261" />


