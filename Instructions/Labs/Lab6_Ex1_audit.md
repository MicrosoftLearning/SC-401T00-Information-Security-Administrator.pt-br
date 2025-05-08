---
lab:
  title: Exercício 1 - Pesquisar o log de auditoria
  module: Module 6 - Audit and search activity in Microsoft Purview
---

## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 6 - Exercício 1 - Pesquisar o log de auditoria

Você é Joni Sherman, administrador de segurança da informação na Contoso Ltd. Como parte do fortalecimento da investigação e da preparação para conformidade da sua organização, você foi solicitado a usar o Microsoft Purview Audit para revisar as alterações na configuração do DLP e garantir que os registros de auditoria de atividades confidenciais sejam mantidos por um período prolongado. Você pesquisará eventos de auditoria relacionados a políticas de DLP, exportará os resultados para análise offline e configurará uma política de retenção de auditoria que preserva registros chave no Exchange, SharePoint e na atividade de pontos de extremidade.

**Tarefas:**

1. Pesquisar atividades relacionadas ao DLP
1. Exportar resultados da pesquisa de auditoria
1. Criar uma política de retenção de auditoria

## Tarefa 1 - Pesquisar atividades relacionadas ao DLP

Nesta tarefa, você usará a solução de Auditoria do Microsoft Purview para pesquisar eventos de auditoria recentes relacionados à política e às regras de DLP.

1. No Microsoft Edge, navegue até `https://purview.microsoft.com` e entre no portal do Microsoft Purview como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. No Microsoft Purview, navegue até **Soluções** > **Auditoria**.

1. Na página **Pesquisar**, configure sua pesquisa:

   - **Intervalo de data e hora (UTC)**:

     - **Data de início**: 3 dias atrás
     - **Data de término**: Hoje

   - **Atividades - nomes amigáveis**: Pesquise por`DLP` e selecione as seguintes atividades em **Atividades de proteção de informações e DLP**:

     - Regra DLP criada
     - Regra DLP atualizada
     - Regra DLP excluída
     - Política DLP criada
     - Política de DLP atualizada
     - Excluir uma política DLP

   ![Captura de tela mostrando as atividades DLP a serem selecionadas na Auditoria.](../Media/audit-dlp-search.png)

   - **Pesquisar nome**: `DLP Policy Activity`

1. Selecione **Pesquisar**.

1. A pesquisa pode demorar alguns minutos a ser concluída. Enquanto a Auditoria processa sua pesquisa, atualize a página para verificar o **Status da tarefa**, **Progresso (%)** e **Tempo de pesquisa**.

1. Após concluir, selecione **Atividade da política DLP** para visualizar os resultados.

1. Selecione resultados individuais para exibir informações detalhadas sobre cada atividade DLP.

Você pesquisou e revisou a atividade de auditoria relacionada à política DLP e à configuração de regras.

## Tarefa 2 – Exportar resultados da pesquisa de auditoria

Nesta tarefa, você exportará os resultados da pesquisa de auditoria DLP para análise offline ou manutenção de registros de conformidade.

1. No Microsoft Purview, navegue até **Soluções** > **Auditoria**.

1. Na página **Pesquisar**, selecione a pesquisa **Atividade da política de DLP** criada na tarefa anterior.

1. Na parte superior da página, selecione **Iniciar**.

1. Na caixa de diálogo de confirmação, selecione **OK** para iniciar a exportação.

1. Quando a exportação for concluída, selecione o link **Baixar arquivo** no banner verde **Sua exportação foi concluída**.

 > [!Note] **Observação**: os arquivos de exportação de auditoria são salvos no formato CSV e podem ser abertos em qualquer editor de texto ou aplicativo de planilha. Para facilitar a revisão, use o Excel ou outra ferramenta de planilha. Neste ambiente de laboratório, você pode abrir o CSV no Bloco de Notas para confirmar se a exportação foi concluída com êxito.

Você exportou logs de auditoria relacionados à DLP, que podem ser usados para revisão offline ou manutenção de registros.

## Tarefa 3 -Criar uma política de retenção de auditoria

Nesta tarefa, você configurará uma política de retenção de auditoria para preservar logs relacionados a correspondências e ações de DLP para investigação de longo prazo.

1. No Microsoft Purview, navegue até **Soluções** > **Auditoria**.

1. Selecione **Políticas** na barra lateral esquerda.

1. Na página **Políticas**, selecione **Nova política de retenção de auditoria**.

1. No painel **Nova política de retenção de auditoria**, insira:

   - **Nome da política**: `Retain DLP Audit Logs`
   - **Descrição**: `Retains audit logs for DLP activities across Exchange, SharePoint, and endpoints to support investigation and compliance.`
   - **Usuários**: deixe em branco para aplicar a todos os usuários
   - **Tipo de Registro**:
      - ComplianceDLPEndpoint
      - ComplianceDLPExchange
      - ComplianceDLPExchangeClassification
      - ComplianceDLPSharePoint
      - ComplianceDLPSharePointClassification
   - **Duração**: 1 ano
   - **Prioridade**:`1`

1. Selecione **Salvar** para criar a política de retenção de auditoria.

Você configurou uma política de retenção de auditoria que mantém logs de correspondências e atividades de DLP por um ano.
