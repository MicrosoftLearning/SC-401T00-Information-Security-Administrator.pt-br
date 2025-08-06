---
lab:
  title: 'Exercício 1: implementar e gerenciar políticas DLP'
  module: Module 2 - Implement Data Loss Prevention
---
## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 2 – Exercício 1: implementar e gerenciar políticas DLP

Joni Sherman, o recém-contratado Administrador de Segurança da Informação da Contoso Ltd., foi solicitado a configurar políticas de DLP (prevenção contra perda de dados) para ajudar a proteger dados confidenciais do cliente no Microsoft 365. Neste laboratório, você usará o Microsoft Purview e o Microsoft Defender para criar e gerenciar políticas DLP que detectam e restringem o compartilhamento de informações confidenciais, como números de cartão de crédito e IDs de funcionários.

**Tarefas:**

1. Criar uma política DLP no modo de simulação
1. Modificar uma política DLP
1. Criar uma política DLP no PowerShell
1. Ativar uma política no modo de simulação
1. Modificar a prioridade da política
1. Habilitar a inspeção de arquivos no Microsoft 365 Defender
1. Criar uma política do Microsoft 365 Defender para arquivos

## Tarefa 1 – Criar uma política DLP no modo de simulação

Nesta tarefa, você criará uma política DLP no modo de simulação que tem como alvo números de cartão de crédito em mensagens do Teams. A política notificará os usuários quando eles tentarem compartilhar conteúdo confidencial e permitirá que eles substituam com justificativa.

1. Entra na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**.

1. No **Microsoft Edge**, vá até **`https://purview.microsoft.com`** e entre no portal do Microsoft Purview como **Joni Sherman**. Entre como `JoniS@WWLxZZZZZZ.onmicrosoft.com`, (em que zzzzzz é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. Clique em **Soluções** > **Prevenção contra perda de dados** > **Políticas**.

1. Na página **Políticas**, escolha **+ Criar política** para iniciar a configuração para criar uma nova política de prevenção contra perda de dados.

1. Na página **Escolher que tipo de dados proteger**, selecione **Dados armazenados em fontes conectadas** e, em seguida, selecione **Avançar**.

1. Na página **Iniciar com um modelo ou criar uma política personalizada**, escolha **Personalizada** como a categoria e, em seguida, **Política personalizada** em **Regulamentos**.

1. Selecione **Avançar**.

1. Na página **Nomear a sua política de DLP**, insira:

   - **Nome**: `DLP - Credit Card Protection`
   - **Descrição**: `Detect and restrict sharing of credit card numbers in Teams messages.`

1. Selecione **Avançar**.

1. Na página **Atribuir unidades de administração**, clique em **Avançar**.

1. Na página **Escolher locais para aplicar a política**, habilite o local somente para **Mensagens de chat e canal do Teams**. Se outros locais estiverem selecionados, desmarque-os.

1. Selecione **Avançar**.

1. Na página **Definir configurações de política**, selecione **Criar ou personalizar regras avançadas de DLP** e selecione **Avançar**.

1. Na página **Personalizar regras avançadas de DLP**, escolha **+ Criar regra**.

1. No submenu **Criar regra**:
    - No campo **Nome**, insira `Credit card information`.

1. Clique em **Condições**, selecione **+Adicionar condição** > **O conteúdo é compartilhado do Microsoft 365**.

1. Na seção **O conteúdo é compartilhado do Microsoft 365**:
    - Selecione a opção com **pessoas de fora da minha organização**.

1. Selecione **+ Adicionar condição** > **O conteúdo contém**.

1. Na nova seção **Conteúdo contém**:
    - Selecione **Adicionar** > **Tipos de informações confidenciais**.
    - Na página **Tipos de informações confidenciais**, pesquise e selecione `Credit Card Number`. Em seguida, selecione **Adicionar**.

1. Em **Ações**, selecione **+ Adicionar uma ação** > **Restringir ou criptografar o conteúdo em locais do Microsoft 365**.

1. Na seção **Restringir o acesso ou criptografar o conteúdo**:
    - Selecione **Bloquear apenas pessoas fora da sua organização**.

1. Em **Notificações do usuário**:
    - Ative a opção **Usar notificações para informar seus usuários e ajudar a instruí-los sobre o uso adequado de informações confidenciais.**.
    - Selecione a caixa de seleção para **Notificar usuários no serviço Office 365 com uma dica de política**.

1. Em **Substituições do usuário**:
    - Selecione a caixa de seleção **Permitir que os usuários substituam as restrições da política** (Fabric, Exchange, SharePoint, OneDrive e Teams).
    - Selecione a caixa de seleção para **Exigir uma justificativa comercial para substituir**.

1. Em **Relatórios de incidentes**, no menu suspenso **Usar este nível de gravidade em alertas e relatórios administrativos**:
    - Selecione **Baixo**.

1. Na parte inferior do painel de submenu **Criar regra**, clique em **Salvar**.

1. De volta à página **Personalizar regras avançadas de DLP**, clique em **Avançar**.

1. Na página **Modo de política**, escolha **Executar a política no modo de simulação** e marque a caixa de seleção **Mostrar dicas de política no modo de simulação**.

1. Selecione **Avançar**.

1. Na página **Revisar e concluir**, revise as configurações e clique em **Enviar**.

1. Na página **Nova política criada**, selecione **Concluído**.

Você criou uma política de DLP que verifica o conteúdo do Teams em busca de números de cartão de crédito e permite substituições com justificativa comercial.

## Tarefa 2 – Modificar uma política de DLP

Nesta tarefa, você expandirá o escopo de sua política de DLP existente para incluir emails do Exchange. Isso ajuda a garantir uma proteção consistente em canais de comunicação adicionais.

1. Você ainda deve estar na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e no Microsoft 365 como **Joni Sherman**.

1. Você ainda deve estar na página **Políticas** do Microsoft Purview. Se não estiver, abra o **Microsoft Edge** e navegue até `https://purview.microsoft.com`. Clique em **Soluções** > **Prevenção contra perda de dados** > **Políticas**.

1. Na página **Políticas**, marque a caixa de seleção para o **DLP — Proteção de cartão de crédito** criado recentemente e selecione **Editar política** para abrir a configuração da política.

1. Na página **Nomear sua política de DLP**, edite a descrição para `Detect and restrict sharing of credit card numbers in Teams and Exchange messages.`

1. Selecione **Avançar**.

1. Na página **Atribuir unidades de administração**, clique em **Avançar**.

1. Na página **Escolher locais para aplicar a política**, marque a caixa de seleção **Email do Exchange** para adicionar esse local à sua política DLP.

1. Clique em **Avançar** até chegar à página **Revisar e concluir**.

1. Clique em **Enviar** na página **Revisar e concluir** para aplicar a alteração feita na política.

1. Depois que a política for atualizada, clique em **Concluído** na página **Política atualizada**.

Você atualizou com êxito a política para verificar emails junto com mensagens do Teams.

## Tarefa 3 – Criar uma política DLP no PowerShell

Nesta tarefa, você criará uma política de DLP usando o PowerShell para bloquear o compartilhamento de IDs de funcionários por email. Essa abordagem demonstra como definir e impor configurações de política por meio de scripts.

1. Você ainda deve estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**.

1. Abra uma janela do PowerShell com privilégios elevados clicando com o botão direito do mouse no botão **Iniciar** na barra de tarefas e selecionando **Terminal (Administrador)**.

1. Execute o cmdlet **Connect-IPPSSession** para se conectar ao PowerShell de Segurança e Conformidade:

    ```powershell
    Connect-IPPSSession
    ```

1. Entre como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (onde ZZZZZZ é o seu ID de locatário exclusivo fornecido pelo provedor de hospedagem do seu laboratório) na janela pop-up **Entrar na sua conta**. A senha de Joni foi definida em um exercício anterior.

1. Execute o **cmdlet New-DlpCompliancePolicy** para criar uma política DLP que verifica todas as caixas de correio do Exchange:

    ```powershell
    New-DlpCompliancePolicy -Name "EmployeeID DLP Policy" -Comment "This policy blocks sharing of Employee IDs" -ExchangeLocation All
    ```

1. Execute o cmdlet **New-DlpComplianceRule** para adicionar uma regra DLP à política DLP criada na etapa anterior. Esta política usa o tipo de informação confidencial **IDs de funcionários da Contoso** criado em um exercício anterior:

    ```powershell
    New-DlpComplianceRule -Name "EmployeeID DLP rule" -Policy "EmployeeID DLP Policy" -BlockAccess $true -ContentContainsSensitiveInformation @{Name="Contoso Employee IDs"}
    ```

1. Execute o cmdlet **Get-DLPComplianceRule** para examinar a **Regra DLP EmployeeID**:

    ```powershell
    Get-DLPComplianceRule -Identity "EmployeeID DLP rule"
    ```

Você usou com êxito o PowerShell para criar uma política DLP que bloqueia o compartilhamento de IDs de funcionários.

## Tarefa 4 – Ativar uma política no modo de simulação

Agora que sua política DLP foi testada na simulação, você a ativará para começar a impor suas ações.

1. Você ainda deve estar na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e no Microsoft 365 como **Joni Sherman**.

1. No **Microsoft Edge**, navegue até as políticas DLP acessando `https://purview.microsoft.com` > **Soluções** > **Prevenção contra perda de dados** e clique em **Políticas** na barra lateral à esquerda.

1. Na página **Políticas**, selecione a política **DLP - Proteção de cartão de crédito**.

1. Na parte inferior do submenu à direita, selecione **Exibir simulação**.

1. Na página de simulação, reserve um momento para explorar:

   - A guia **Visão geral da simulação**, que mostra o progresso da verificação, o total de correspondências e o status da verificação por local.
   - A guia **Itens para revisão**, onde todas as correspondências previstas aparecerão quando estiverem disponíveis.
   - A guia **Alertas**, onde todos os alertas disparados no modo de simulação serão listados.

1. Depois de explorar os insights no modo de simulação, selecione **Ativar a política** e, em seguida, **Confirmar** para ativar a política DLP.

   Um submenu de confirmação será exibido indicando que a política foi publicada.

A política agora está ativa e impondo restrições às informações de cartão de crédito no Teams e no Exchange.

## Tarefa 5 — Modificar a prioridade da política

Quando existem várias políticas, a prioridade delas determina qual delas se aplica primeiro. Nesta tarefa, você mudará a prioridaded a política de ID do funcionário para a prioridade mais alta.

1. Você ainda deve estar na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e no Microsoft 365 como **Joni Sherman**.

1. No **Microsoft Edge**, a guia do portal Microsoft Purview ainda deve estar aberta na página **Políticas**. Se não estiver, abra o **Microsoft Edge** e navegue até `https://purview.microsoft.com`. Clique em **Soluções** > **Prevenção contra perda de dados** > **Políticas**.

1. Na página **Políticas**, selecione a **Política DLP EmployeeID**.

1. Selecione **Repriorizar** na faixa de opções de navegação superior e, em seguida, selecione **Mover para o topo (prioridade mais alta)**.

1. Na janela **Prevenção contra perda de dados**, selecione **Atualizar** e revise a prioridade na coluna **Ordem** da tabela de políticas.

1. Saia da conta de Joni selecionando seu ícone no canto superior direito e, em seguida, selecione **Sair**.

Você atualizou a prioridade da política para que a política de ID do funcionário tenha precedência sobre as outras.

## Tarefa 6 — Habilitar a inspeção de arquivos no Microsoft 365 Defender

Algumas políticas de arquivo exigem acesso para inspecionar o conteúdo de arquivos protegidos. Nesta tarefa, você concederá as permissões necessárias para permitir que o Microsoft Defender verifique o conteúdo dos arquivos do OneDrive e do SharePoint em busca de informações confidenciais.

1. Você ainda deve estar na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e conectado como Joni Sherman.

1. No **Microsoft Edge**, navegue até o Microsoft Defender acessando `https://security.microsoft.com`. Entre como **Administrador MOD**, `admin@WWLxZZZZZZ.onmicrosoft.com`, (em que zzzzzz é a sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.

1. Na barra lateral esquerda, selecione **Sistema** > **Configurações** e, em seguida, selecione **Aplicativos de nuvem**.

1. No painel esquerdo, na janela **Aplicativos de nuvem**, role para baixo até a seção **Proteção de informações**. Em **Inspecionar arquivos protegidos**, selecione **Conceder permissão** para habilitar a inspeção de arquivos.

1. Siga o prompt para permitir as permissões necessárias no Microsoft Entra ID e, em seguida, você verá que a inspeção de arquivo está **Ativa** no Microsoft Defender para Aplicativos de Nuvem.

1. Saia da conta de Administrador MOD clicando no ícone **MA** no canto superior direito, selecione **Sair** e feche a janela do navegador.

A inspeção de arquivos agora está habilitada no Defender, permitindo que as políticas de arquivos verifiquem conteúdo confidencial.

## Tarefa 7 — Criar uma política de arquivo para o Microsoft 365 Defender

Nesta tarefa, você criará uma política de arquivo no Microsoft Defender que identifica e coloca em quarentena arquivos que contêm números de cartão de crédito no OneDrive e no SharePoint.

1. Você ainda deve estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**.

1. Abra o **Microsoft Edge** e navegue até **`https://security.microsoft.com`** para entrar no portal do Microsoft Defender como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. No portal **Microsoft Defender**, na navegação à esquerda, selecione **Aplicativos de nuvem** > **Políticas** e, em seguida, selecione **Gerenciamento de políticas**.

1. Na página **Políticas**, selecione **+ Criar política** e selecione a **Política de arquivo**.

1. Na página **Criar política de arquivo
**, configure:

   - **Nome da política**: `Credit card information for files`
   - **Gravidade da política**: **Baixa**
   - **Categoria**: **DLP**
   - **Descrição**: `Protect credit card numbers from being shared in files.`
   - Na seção **Arquivos que correspondem a todos os seguintes**:
      - Para o primeiro filtro, configure os menus suspensos para: **Nível de acesso igual a Público (Internet), Externo, Público** e adicione **Interno**
      - Para o segundo filtro, configure os menus suspensos para: **Última modificação após (data)** e use a data de hoje

          ![Captura de tela mostrando o menu suspenso de correspondência de arquivos com a opção interna adicionada.](../Media/files-matching-internal.png)

   - No menu suspenso **Método de inspeção**, selecione **Serviço de classificação de dados**.
   - No menu suspenso **Escolher tipo de inspeção...**, selecione **Tipo de informação confidencial...**.
   - Na caixa de diálogo **Selecionar um tipo de informação confidencial**, pesquise e marque a caixa de seleção `Credit Card Number`.
      - Selecione **Concluído** no canto superior direito da caixa de diálogo **Selecionar um tipo de informação confidencial**.

   - Em **Ações de governança**, expanda **Microsoft OneDrive for Business**:
      - Marque a caixa de seleção **Colocar em quarentena de usuário**
   - Repita o mesmo processo para o **Microsoft SharePoint Online**
      - Marque a caixa de seleção **Colocar em quarentena de usuário**

1. Selecione **Criar** na parte inferior da página para criar a política de arquivo.

Você criou com êxito uma política de arquivos que detecta e coloca em quarentena arquivos com dados confidenciais de cartão de crédito.
