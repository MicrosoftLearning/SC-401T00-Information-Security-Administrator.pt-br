---
lab:
  title: Exercício 1 — Proteger dados em ambientes de IA
  module: Module 4 - Protect data in AI environments
---

## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 4 — Exercício 1 — Proteger dados em ambientes de IA

Você é Joni Sherman, administrador de segurança da informação da Contoso Ltd. Já que ferramentas de IA como o Microsoft Copilot se tornam mais integradas aos fluxos de trabalho diários, foi solicitado que a sua equipe avalie e melhore as proteções em torno de dados confidenciais. Neste laboratório, você explorará como o DSPM para IA do Microsoft Purview pode ajudar a proteger as interações de dados com ferramentas de IA por meio da imposição de políticas, detecção de riscos e avaliações de exposição.

**Tarefas:**

1. Usar o DSPM para IA para criar uma política DLP para sites de IA generativa
1. Criar uma política de risco interno para detectar interações arriscadas de IA
1. (Opcional) Impedir que o Copilot acesse o conteúdo rotulado
1. Executar uma avaliação de dados para detectar conteúdo não rotulado

## Tarefa 1 — Usar o DSPM para IA para criar uma política DLP para sites de IA generativa

Para reduzir o risco de perda de dados com assistentes de IA, você começará criando uma política DLP usando a recomendação de segurança de dados do Fortify. Esta política usa a Proteção adaptável para restringir a colagem ou o upload de dados confidenciais em ferramentas de IA como ChatGPT e Copilot no Edge, Chrome e Firefox.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin**.

1. No **Microsoft Edge**, vá até **`https://purview.microsoft.com`** e entre como **Joni Sherman**, `JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório).

1. No Microsoft Purview, navegue até o DSPM para IA selecionando **Soluções** > **DSPM para IA** > **Recomendações**

1. Selecione a recomendação de **segurança de dados do Fortify**.

1. Na página de submenu **Segurança de dados para IA**, revise o resumo e selecione **Criar políticas**. Isso criará uma política DLP pré-configurada voltada para sites de IA generativa.

1. Depois que a política for criada, selecione **Exibir política**.

1. Na seção **Detalhes da política**, selecione **Editar política na solução** para abrir a solução **Prevenção contra perda de dados** no Microsoft Purview.

1. Na página **Políticas**, localize e selecione a política **DSPM para IA — Bloquear informações confidenciais de sites de IA**.

1. No submenu, selecione **Exibir simulação**.

1. No painel de simulação, selecione **Editar a política**.

1. Selecione **Avançar** até chegar à página **Escolher onde aplicar a política**. Confirme se a política está no escopo de **Dispositivos**.

1. Selecione **Avançar**.

1. Na página **Personalizar regras de DLP avançadas**, selecione o ícone de lápis ao lado de **Bloquear com substituição para usuários de risco elevado** para visualizar a regra.

1. Examine a configuração da regra criada pelo DSPM para IA:
   - Em **Condições**, observe os tipos de informações confidenciais incluídos e que a regra usa **Proteção adaptável** com base no risco elevado.
   - Em **Ações**, confirme se **as atividades do domínio do serviço e do navegador** estão definidas como **Bloquear com substituição** para **Sites de IA generativa**.

1. Selecione **Cancelar** para sair do editor de regras sem alterações.

1. De volta à página **Personalizar regras avançadas de DLP**, selecione **Avançar**.

1. Na página **Modo da política**, selecione **Ativar a política se ela não for editada dentro de quinze dias após a simulação** e selecione **Avançar**.

1. Na página **Revisar e concluir**, clique em **Enviar** e, em seguida, selecione **Concluído**.

Você criou uma política que impede que usuários de alto risco compartilhem dados confidenciais em sites de IA generativa e confirmou a configuração de política definida pelo DSPM para IA.

## Tarefa 2 — Criar uma política de risco interno para detectar interações arriscadas de IA

Em seguida, você criará uma política que ajuda a detectar comportamentos de prompt arriscados no Copilot.

1. No Microsoft Purview, navegue até **DSPM para IA** selecionando **Soluções** > **DSPM para IA** > **Recomendações**.

1. Selecione a recomendação **Detectar interações arriscadas em aplicativos de IA (versão prévia)**.

1. Na página de submenu **Detectar interações arriscadas em aplicativos de IA (versão prévia),** revise o resumo e selecione **Criar política**.

1. Depois que a política for criada, selecione **Exibir política**.

1. Na seção **Detalhes da política**, selecione **Editar política na solução** para abrir a área **Gerenciamento de Risco Interno** do Microsoft Purview.

1. Na página **Políticas**, localize e selecione a política **DSPM para IA — Detectar uso arriscado de IA**.

1. No submenu, selecione **Editar política** para revisar a configuração completa da política.

1. Na página **Escolher um modelo de política**, observe que a política usa o modelo **Uso arriscado de IA (pré-visualização)**.

1. Selecione **Avançar** até chegar à **página Escolher evento de acionamento para esta política**.
Confirme se o evento de ativação é **Conta de usuário excluída do Microsoft Entra ID**, que sinaliza riscos potenciais relacionados à desativação que podem preceder ou seguir atividades de IA arriscadas.

1. Selecione **Avançar**.

1. Na página **Indicadores**, expanda as categorias de indicadores para revisar quais sinais estão selecionados:

   - Navegou em sites de IA generativa
   - Recebeu resposta confidencial do Copilot
   - Inserida solicitação arriscada no Copilot

1. Selecione **Avançar** até chegar à página **Revisar e concluir** e, em seguida, selecione **Cancelar** para sair do editor sem fazer alterações.

Você criou uma política que detecta interações de IA arriscadas, incluindo solicitações e respostas, para ajudar a identificar sinais precoces de comportamento arriscado do usuário.

## Tarefa 3 - (Opcional) Impedir que o Copilot acesse o conteúdo rotulado

Você pode reduzir ainda mais o risco impedindo que o Copilot processe ou responda com conteúdo protegido por rótulos de confidencialidade.

1. No Microsoft Purview, navegue até **DSPM para IA** selecionando **Soluções** > **DSPM para IA** > **Recomendações**.

1. Selecione a recomendação **Proteger dados confidenciais referenciados nas respostas do Copilot e do agente**.

1. Revise as diretrizes fornecidas nesta recomendação.

1. Navegue até **Soluções** > **Prevenção contra perda de dados** > **Políticas**.

1. Selecione **+ Criar política** e, em seguida, escolha **Política personalizada**.

1. Na página **Nomear a sua política de DLP**, insira:

   - **Nome**: `DLP - Block Copilot access to labeled content`
   - **Descrição**: `Prevents Microsoft 365 Copilot from processing or responding with content labeled using sensitivity labels.`

1. Selecione **Avançar** até chegar à página **Escolher onde aplicar a política**.

1. Selecione **Microsoft 365 Copilot (pré-visualização)** como o escopo da política e, em seguida, selecione **Avançar** até chegar à página **Personalizar regras avançadas de DLP**.

1. Selecione **Criar regra** e configure:

   - **Nome**: `Prevent Copilot from accessing labeled data`
   - Em **Condições**, selecione **Adicionar condição** > **Conteúdo contém** > **Rótulos de confidencialidade**. Adicione estes rótulos de confidencialidade:
     - `Internal`
     - `Confidential`
     - `Highly Confidential`
   - Selecione **Adicionar**
   - Em **Ações**, selecione **Adicionar uma ação** > **Impedir que o Copilot processe conteúdo (visualização)**
   - Selecione **Salvar** na parte inferior do submenu **Criar regra**.

1. De volta à página **Personalizar regras avançadas de DLP**, selecione **Avançar**.

1. Na página **Modo de política**, selecione **Ativar a política imediatamente** e, em seguida, selecione **Avançar**.

1. Na página **Revisar e concluir**, selecione **Enviar** e, em seguida, selecione **Concluído** na página **Nova política criada**.

1. Volte para **DSPM para recomendações de IA** selecionando **Soluções** > **DSPM para IA** > **Recomendações**.

1. Selecione a recomendação **Proteger dados confidenciais referenciados nas respostas do Copilot e do agente** e selecione **Marcar como concluído**.

Você criou uma política de DLP que impede que o conteúdo rotulado seja usado nas solicitações e respostas do Copilot.

## Tarefa 4 — Executar uma avaliação de dados para detectar conteúdo não rotulado

Para entender possíveis lacunas na cobertura de rotulagem, você executará uma avaliação de risco de dados para identificar arquivos sem rótulos de confidencialidade que podem ser acessados pelo Copilot.

1. Em **DSPM para IA**, selecione a recomendação intitulada **Proteger dados confidenciais referenciados nas respostas do Copilot e do agente**.

1. No painel **Proteger dados confidenciais referenciados nas respostas do Copilot e do agente**, revise o resumo e selecione **Ir para avaliações**.

1. Na página **Avaliações de risco de dados**, selecione **Criar avaliação personalizada**

1. Na página **Detalhes básicos**, insira:

   - **Nome**: `Unlabeled File Exposure Assessment`
   - **Descrição**: `Identifies files without sensitivity labels that may be exposed in Microsoft 365 Copilot responses and provides recommendations to reduce oversharing risks.`

1. Selecione **Avançar**.

1. Na página **Adicionar usuários**, selecione **Todos** e, em seguida, selecione **Avançar**.

1. Na página **Adicionar fontes de dados para avaliar**, deixe o local padrão **SharePoint** selecionado e selecione **Avançar**.

1. Na página **Revisar e executar o exame de avaliação de dados**, selecione **Salvar e executar**.

1. Na página **Avaliação de dados criada com sucesso**, selecione **Concluído**.

Agora você usou o DSPM do Microsoft Purview para IA para detectar riscos relacionados à IA, impor políticas e avaliar a exposição de dados confidenciais, ajudando a sua organização a usar a IA com segurança.
