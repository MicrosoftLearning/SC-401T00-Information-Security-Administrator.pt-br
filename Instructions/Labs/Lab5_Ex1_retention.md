---
lab:
  title: Exercício 1 — Configurar políticas de retenção
  module: Module 5 - Implement and manage retention
---

## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 5 — Exercício 1 — Implementar e gerenciar a retenção

Você é Joni Sherman, Administradora de Conformidade da Contoso Ltd. A empresa está reforçando a estratégia de segurança de dados para reduzir a exposição ao risco relacionada a dados financeiros e comunicações privilegiadas. Foi solicitado que você configure soluções de retenção do Microsoft Purview que dão suporte à preparação para auditoria, limitam a retenção de dados desnecessária e garantem a supervisão adequada para comunicações confidenciais.

**Tarefas:**

1. Criar um rótulo de retenção
1. Publicar um rótulo de retenção
1. Criar uma política de rótulo de retenção de aplicação automática
1. Criar uma política de retenção estática
1. Criar um escopo adaptável
1. Criar uma política de retenção adaptável
1. Recuperar conteúdo do SharePoint

## Tarefa 1 — Criar um rótulo de retenção

Nesta tarefa, você criará um rótulo de retenção para dados financeiros confidenciais que precisam ser retidos para fins de auditoria e investigação.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin**.

1. No Microsoft Edge, navegue até `https://purview.microsoft.com` e entre no portal do Microsoft Purview como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. Navegue até **Soluções** > **Gerenciamento do Ciclo de Vida dos Dados** > **Rótulos de retenção**.

1. Na página **Rótulos**, selecione **Criar um rótulo**.

1. Na página **Nomear rótulo de retenção**, insira:

   - **Nome**: `Sensitive Financial Records`
   - **Descrição para usuários**: `Use for financial files with sensitive data that must be retained for audit or security purposes.`
   - **Descrição para administradores**: `Retains high-impact financial data for 5 years to support audits and security investigations.`

1. Selecione **Avançar**.

1. Na página **Definir configurações de rótulo**, escolha **Reter itens para sempre ou por um período específico** e clique em **Avançar**.

1. Na página **Definir o período**, verifique se esses valores estão definidos para a entrada de configuração do período de retenção:

    - **Quanto tempo dura o período?**: cinco anos
    - **Quando o período deve começar?**: quando os itens foram modificados

1. Selecione **Avançar**.

1. Na página **Escolher o que acontece após o período de retenção**, selecione **Excluir itens automaticamente** e **Avançar**.

1. Na página **Revisar e concluir**, selecione **Criar rótulo**.

1. Na página **Seu rótulo de retenção foi criado**, selecione a opção **Não fazer nada** e, em seguida, **Concluído**.

Você criou um rótulo de retenção que retém o conteúdo financeiro por cinco anos e o exclui posteriormente para reduzir a exposição dos dados.

## Tarefa 2 — Publicar um rótulos de retenção

Nesta tarefa, você publicará o rótulo de retenção para que os usuários possam aplicá-lo em serviços do Microsoft 365, como o Exchange, SharePoint e OneDrive.

1. No Microsoft Purview, navegue até **Soluções** > **Gerenciamento do Ciclo de Vida dos Dados** > **Rótulos de retenção**.

1. Marque a caixa de seleção ao lado do rótulo **Registros financeiros confidenciais** e selecione o ícone **Publicar rótulos** (![Ícone Publicar rótulos](../Media/publish-labels-icon.png)) para publicar este rótulo de retenção.

1. Na página **Escolher rótulos para publicar**, verifique se o rótulo **Registros financeiros confidenciais** está selecionado e selecione **Avançar**.

1. Na página **Escopo da política**, clique em **Avançar**.

1. Na página **Escolher o tipo de política de retenção para criar**, selecione **Estática ** e clique em **Avançar**.

1. Na página **Escolher onde publicar rótulos**, selecione **Deixar que eu escolha locais específicos** e selecione:

    - Caixas de correio do Exchange
    - Sites clássicos e de comunicação do SharePoint
    - Contas do OneDrive
    - Desmarque todos os outros locais

1. Selecione **Avançar**.

1. Na página **Nomear política**, insira:

    - **Nome**: `Sensitive Financial Data Retention`
    - **Descrição**: `Makes the 'Sensitive Financial Records' label available to users in Exchange, SharePoint, and OneDrive.`

1. Selecione **Avançar**.

1. Na página **Concluir**, clique em **Enviar**.  

1. Na página **Seu rótulo de retenção foi publicado,** clique em **Concluído**.

Você publicou o rótulo de retenção, disponibilizando-o para os usuários aplicarem nos principais serviços do Microsoft 365.

## Tarefa 3 — Criar uma política de rótulo de retenção de aplicação automática

Nesta tarefa, você configurará uma política que aplica automaticamente um rótulo de retenção ao conteúdo que contém informações financeiras pessoais.

1. No Microsoft Purview, navegue até **Soluções** > **Gerenciamento do Ciclo de Vida dos Dados** > **Políticas** > **Políticas de rótulo**.

1. Na página **Políticas de rótulo**, selecione **Aplicar automaticamente um rótulo** para iniciar a configuração do rótulo.

1. Na **página de Introdução**, insira:

   - **Nome**: `Auto-apply Personal Financial PII`
   - **Descrição**: `Applies this label to personal financial data to help meet audit and investigation requirements. Retains content for 3 years.`

1. Selecione **Avançar**.

1. Na página **Escolher o tipo de conteúdo ao qual você deseja aplicar este rótulo**, selecione **Aplicar rótulo ao conteúdo que contém informações confidenciais** e selecione **Avançar**.

1. Na página **Conteúdo que contém informações confidenciais**, selecione a categoria **Financeiras**, depois selecione o regulamento **U.S. Gramm-Leach-Bliley Act (GLBA)** e selecione **Avançar**.

1. Na página **Definir conteúdo que contém informações confidenciais**, selecione **Avançar**.

1. Na página **Escopo da política**, clique em **Avançar**.

1. Na página **Escolher o tipo de política de retenção a ser criada**, selecione **Estática**.

1. Na página **Escolher onde publicar rótulos**, selecione **Deixar que eu escolha locais específicos** e selecione:

    - Caixas de correio do Exchange
    - Sites clássicos e de comunicação do SharePoint
    - Contas do OneDrive
    - Desmarque todos os outros locais

1. Na página **Escolher um rótulo para aplicar automaticamente**, selecione **Adicionar rótulo**.

1. No submenu **Escolher um rótulo**, selecione **PII financeias pessoais** e, em seguida, **Adicionar**.

1. De volta à página **Escolher um rótulo para aplicar automaticamente**, clique em **Avançar**.

1. Na página **Decidir se deseja testar ou executar a política**, selecione **Testar a política antes de executá-la** e selecione **Avançar**.

1. Na página **Revisar e concluir**, selecione **Enviar** e, em seguida, selecione **Concluído** na página **Sua política de aplicação automática foi criada**.

Você criou uma política de aplicação automática que identifica dados financeiros pessoais e aplica um rótulo de retenção automaticamente.

## Tarefa 4 — Criar uma política de retenção estática

Nesta tarefa, você criará uma política de retenção estática para o conteúdo do Microsoft Teams para ajudar a reduzir o risco de dados a longo prazo.

1. No Microsoft Purview, navegue até **Soluções** > **Gerenciamento do Ciclo de Vida dos Dados** > **Políticas** > **Políticas de retenção**.

1. Na página **Políticas de retenção**, selecione **Nova política de retenção**.

1. Na página **Nomear política de retenção**, insira:

   - **Nome**: `Teams Retention`
   - **Descrição**: `Retains Teams chats and channel messages for 3 years, then deletes them to reduce long-term data risk.`

1. Selecione **Avançar**.

1. Na página **Escopo da política**, clique em **Avançar**.

1. Na página **Escolher o tipo de política de retenção para criar**, selecione **Estática** e clique em **Avançar**.

1. Na página **Escolher locais para aplicar a política**, habilite:

   - Mensagens do canal do Teams
   - Chats do Teams
   - Desabilitar todos os outros locais.

1. Selecione **Avançar**.

1. Na página **Decidir se deseja reter o conteúdo, excluí-lo ou ambos**, verifique se esses valores estão definidos para a configuração de retenção:

   - Selecione **Reter itens por um período específico**.
   - Em **Reter itens por um período específico**, selecione **Personalizado** na lista suspensa.
   - Altere o campo de anos para `3`
   - **Iniciar o período de retenção com base em**: quando os itens foram alterados pela última vez
   - **Ao final do período de retenção**: excluir itens automaticamente

1. Selecione **Avançar**.

1. Na página **Revisar e concluir**, selecione **Enviar** e, em seguida, **Concluído** na página **Você criou uma política de retenção com êxito**.

Você configurou uma política de retenção estática que retém mensagens do Teams por três anos antes de excluí-las automaticamente.

## Tarefa 5: criar um escopo adaptável

Nesta tarefa, você definirá um escopo adaptável direcionado a grupos do Microsoft 365 associados a funções de liderança e operações.

1. No Microsoft Purview, **Configurações** > **Funções e escopos** > **Escopos adaptáveis.**

1. Na página **Escopos adaptáveis**, selecione **+ Criar escopo**.

1. Na página **Nomear o escopo da política adaptativa**, insira:

    - **Nome**: `Leadership and Ops Groups`
    - **Descrição**: `Targets Leadership and Operations M365 groups with privileged access to sensitive data.`

1. Selecione **Avançar**.

1. Na página **Atribuir unidade administrativa**, clique em **Avançar**.

1. Na página **Que tipo de escopo você deseja criar?**, selecione **Usuários** e, em seguida, **Avançar**.

1. Na página **Criar a consulta para definir usuários**, na seção **Atributos do usuário**, verifique se esses valores estão selecionados para a configuração do atributo do usuário:

   - Selecione o menu suspenso **Atributo** e **Departamento**
   - Deixe o valor padrão **é igual a** no próximo campo
   - Insira `Leadership` como o **Valor**.

1. Adicione um segundo atributo selecionando **+ Adicionar atributo** na página **Criar a consulta para definir usuários**. No novo campo sob o que acabamos de configurar, configure estes valores:

   - Selecione a lista suspensa do operador de consulta e atualize-a de E para **Ou**
   - Selecione o menu suspenso **Atributo** e **Departamento**
   - Deixe o valor padrão **é igual a** no próximo campo
   - Insira `Operations` como o **Valor**

1. Selecione **Avançar**.

1. Na página **Examinar e concluir**, selecione **Enviar**.

1. Depois que o escopo adaptável for criado, selecione **Concluído** na página **Seu escopo foi criado**.

Você criou um escopo adaptável a fim de dar suporte à retenção direcionada para grupos privilegiados na organização.

## Tarefa 6: criar uma política de retenção com escopo adaptável

Nesta tarefa, você usará o escopo adaptável criado a fim de configurar uma política de retenção para grupos do Microsoft 365 com responsabilidades confidenciais.

1. No Microsoft Purview, vá até **Soluções** > **Gerenciamento do Ciclo de Vida dos Dados** > **Políticas** >  **Políticas de retenção**.

1. Na página **Políticas de retenção**, selecione **+ Nova política de retenção**.

1. Na página **Nomear política de retenção**, insira:

    - **Nome**: `Privileged Group Retention`
    - **Descrição**: `Retains content from Leadership and Operations groups for 5 years to support audit and investigation.`

1. Selecione **Avançar**.

1. Na página **Escopo da política**, clique em **Avançar**.

1. Na página **Escolher o tipo de política de retenção para criar**, selecione **Adaptável** e, em seguida, **Avançar**.

1. Na página **Escolher escopos de política adaptáveis e locais**, selecione **+Adicionar escopos**.

1. No painel do submenu **Escolher escopos de política adaptáveis**, marque a caixa de seleção **Grupos de Liderança e Operações** e, em seguida, selecione **Adicionar** na parte inferior do painel.

1. Em **Escolher locais para aplicar a política**, habilite:

    - Caixas de correio do Grupo do Microsoft 365 e sites
    - Desabilitar todos os outros locais.

1. Selecione **Avançar**.

1. Na página **Decidir se deseja reter o conteúdo, excluí-lo ou ambos**, verifique se esses valores estão definidos para a configuração de retenção:

   - Selecione **Reter itens por um período específico**.
   - Em **Reter itens por um período específico**, selecione **5 anos** na lista suspensa
   - **Iniciar o período de retenção com base em**: quando os itens foram alterados pela última vez
   - **Ao final do período de retenção**: excluir itens automaticamente

1. Selecione **Avançar**.

1. Na página **Examinar e concluir**, selecione **Enviar**.

1. Selecione **Concluído** assim que a política for criada.

Você criou uma política de retenção que se aplica ao conteúdo pertencente a grupos privilegiados, mantendo-o por cinco anos antes da exclusão.

## Tarefa 7 - Recuperar conteúdo do SharePoint

Nesta tarefa, você simulará a restauração de um documento excluído de um site do SharePoint para validar suas opções de recuperação.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin**.

1. No **Microsoft Edge**, navegue até**`https://www.office.com`** e faça login no Microsoft 365 como **Joni Sherman**.

1. Na página de aterrisagem do Microsoft Office 365, selecione o inicializador de aplicativos (o ícone de grade) no canto superior esquerdo e, em seguida, selecione **SharePoint** no submenu.

   ![Captura de tela mostrando onde as reticências devem ser exibidas para mostrar o menu de ação.](../Media/show-more-actions-sharepoint.png)

1. Na página de aterrisagem do SharePoint, procure por`Benefits` e selecione **Benefícios @ Contoso** nos resultados da pesquisa.

1. Na barra lateral esquerda, selecione **Documentos**.

1. Na página **Documentos**, marque a caixa de seleção para **Políticas de férias.pptx** e selecione **Excluir** na barra de ações.

1. Na caixa de diálogo **Excluir?**, selecione **Excluir**.

1. Na barra lateral esquerda, selecione **Lixeira**.

1. Na página **Lixeira**, clique com o botão direito do mouse em **Políticas de férias.pptx** e selecione **Restaurar**.

1. Na barra lateral esquerda, selecione **Documentos** e observe que o arquivo foi restaurado.

Você recuperou com êxito um documento excluído de um site do SharePoint.

Você restaurou o conteúdo excluído do SharePoint, validando a recuperação de documentos em caso de exclusão acidental ou não autorizada.
