---
lab:
  title: Configuração do laboratório — Preparar seu ambiente para administração
  module: Lab setup
---

## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Configuração do laboratório — Preparar seu ambiente para administração

Neste laboratório, você configurará e preparará seu ambiente para tarefas de administração. Você ativará os recursos necessários, configurará permissões administrativas e garantirá a configuração adequada dos principais elementos.

**Tarefas:**

1. Habilitar a Auditoria no portal do Microsoft Purview
1. Definir senhas de usuário para exercícios de laboratório
1. Habilitar a integração de dispositivos
1. Habilitar a análise de risco interno

## Tarefa 1 – Habilitar a Auditoria no portal do Microsoft Purview

Nesta tarefa, você habilitará a Auditoria no portal do Microsoft Purview para monitorar as atividades do portal.

1. Você ainda deve estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e conectado ao Microsoft 365 com a conta de Administrador do MOD.

1. Abra uma janela elevada do Terminal clicando no botão Windows com o botão direito do mouse e selecione **Terminal (Admin)**.

1. Execute o cmdlet **Install Module** para instalar a versão mais recente do módulo do **PowerShell do Exchange Online**:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```

1. Confirme o prompt do provedor NuGet digitando **Y** para Sim e pressione **Enter**.

1. Confirme a caixa de diálogo Segurança do repositório não confiável com **S** para Sim e pressione **Enter**.  Esse processo pode levar algum tempo para ser concluído.

1. Execute o cmdlet **Set-ExecutionPolicy** para alterar a política de execução e pressione **Enter**.

    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
    ```

1. Feche a janela do PowerShell.

1. Abra uma janela normal (não elevada) do PowerShell clicando com o botão direito do mouse no botão Windows e selecionando **Terminal**.

1. Execute o cmdlet **Connect-ExchangeOnline** para usar o módulo PowerShell do Exchange Online e conectar-se ao seu locatário:

    ```powershell
    Connect-ExchangeOnline
    ```

1. Quando a janela **Entrar** for exibida, entre como `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.

1. Para verificar se a Auditoria está habilitada, execute o cmdlet **Get-AdminAuditLogConfig**:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. Se _UnifiedAuditLogIngestionEnabled_ retornar false, a auditoria estará habilitada.

1. Para habilitar o log de auditoria, execute o cmdlet **Set-AdminAuditLogConfig** e defina **UnifiedAuditLogIngestionEnabled** como _true_:

    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```

1. Para verificar se a Auditoria está habilitada, execute o cmdlet **Get-AdminAuditLogConfig** novamente:

    ```powershell
    Get-AdminAuditLogConfig | FL UnifiedAuditLogIngestionEnabled
    ```

1. _UnifiedAuditLogIngestionEnabled_ retornará _true_ para informar que a auditoria está habilitada.

<!---

1. In Microsoft Edge, navigate to the Microsoft Purview portal, `https://purview.microsoft.com`, and log in.

1. A message about the new Microsoft Purview portal will appear on the screen. Select the option to agree with the terms of data flow disclosure and the privacy statement, then select **Try now**.

    ![Screenshot showing the Welcome to the new Microsoft Purview portal screen.](../Media/welcome-purview-portal.png)

1. Select **Solutions** from the left sidebar, then select **Audit**.

1. On the **Search** page, select the **Start recording user and admin activity** bar to enable audit logging.

    ![Screenshot showing the Start recording user and admin activity button.](../Media/enable-audit-button.png)

1. Once you select this option, the blue bar should disappear from this page.

-->

## Tarefa 2 — Definir senhas de usuário para exercícios de laboratório

Nesta tarefa, você definirá senhas para as contas de usuário necessárias para os laboratórios.

1. Entra na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.

1. Abra o **Microsoft Edge** e navegue até **`https://admin.microsoft.com`** para entrar no centro de administração do Microsoft 365 como Administrador MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem do laboratório).

1. No painel de navegação à esquerda, expanda **Usuários** e selecione **Usuários ativos**.

1. Marque a caixa de seleção à esquerda de **Joni Sherman**, **Lynne Robbins** e **Megan Bowen**.

   Essas contas serão usadas nos exercícios de laboratório.

   ![Captura de tela mostrando contas de usuário que precisam ser redefinidas.](../Media/user-accounts.png)

1. Selecione o botão **Redefinir senha** na navegação superior para redefinir as três senhas.

   ![Captura de tela mostrando o botão Redefinir senha no Centro de administração do Microsoft 365.](../Media/reset-password-button.png)

1. Na página de submenu **Redefinir senha** à direita, verifique se ambas as caixas de seleção estão desmarcadas.

   Isso garantirá que você possa selecionar uma senha para os três usuários que estão sendo usados para exercícios e que essas senhas não precisem ser redefinidas quando você entrar pela primeira vez.

1. No campo **Senha**, digite uma senha que você possa lembrar para redefinir as senhas de usuário a serem usadas em exercícios futuros.

1. Selecione o botão **Redefinir senha** na parte inferior da página **Redefinir senha**.

1. Na página **As senhas foram redefinidas**, você verá as três contas de usuário que foram redefinidas. Na parte inferior desta página de submenu, selecione **Fechar**.

Você redefiniu com sucesso as senhas para exercícios de laboratório.

## Tarefa 3 – Habilitar a integração do dispositivo

Nesta tarefa, você habilitará a integração de dispositivos para sua organização.

1. Ainda é necessário estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e conectado como Administrador MOD no Microsoft 365.

1. No **Microsoft Edge**, navegue até**`https://purview.microsoft.com`** para fazer login no Microsoft Purview e selecione **Configurações** na barra lateral esquerda.

1. Na barra lateral esquerda, expanda **Integração de dispositivos** e selecione **Dispositivos**.

1. Na página **Dispositivos**, selecione **Ativar integração de dispositivos** e, em seguida, selecione **Ok** para habilitar a integração de dispositivos.

1. Quando solicitado, selecione **OK** para confirmar se o monitoramento do dispositivo está sendo ativado.

Agora você habilitou a integração de dispositivos e pode começar a integrar dispositivos a serem protegidos com políticas de DLP de ponto de extremidade. O processo de habilitação do recurso pode levar até 30 minutos.

## Tarefa 4 - Habilitar a análise de riscos internos

Nesta tarefa, você habilitará a análise para o Gerenciamento de risco interno.

1. Ainda é necessário estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e conectado como Administrador MOD no Microsoft Purview.

1. No Microsoft Purview, navegue até **Configurações** > **Gerenciamento de risco interno** > **Análise**.

1. Alterne **Análise** para **Ativado** e selecione **Salvar**.

Você habilitou a análise para Gerenciamento de risco interno.

## Tarefa 5 - Inicializar o Microsoft Defender XDR

Nesta tarefa, você abrirá o Microsoft Defender e aguardará a conclusão da inicialização do Microsoft Defender XDR.

1. Ainda é necessário estar conectado à VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin** e conectado como Administrador MOD no Microsoft Purview.

1. No **Microsoft Edge**, navegue até**`https://security.microsoft.com/`** para abrir o Microsoft Defender.

1. No painel de navegação, selecione **Investigação e resposta** > **Incidentes e alertas** > **Incidentes**.

1. Você verá uma mensagem informando que o Microsoft Defender XDR está sendo preparado. Esse processo é executado automaticamente e pode levar alguns minutos.

   ![Captura de tela mostrando o Microsoft Defender XDR sendo integrado.](../Media/enable-defender-xdr.png)

O Microsoft Defender XDR está sendo inicializado. Você pode continuar com outras tarefas enquanto a configuração é concluída.
