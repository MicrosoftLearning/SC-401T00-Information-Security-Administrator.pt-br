---
lab:
  title: Exercício 1 — Implementar o gerenciamento de risco interno
  module: Module 3 - Implement Insider Risk Management
---

## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 3 — Exercício 1 — Implementar o gerenciamento de risco interno

Você é Joni Sherman, administradora de segurança da informação da Contoso Ltd. Sua função envolve garantir a conformidade regulatória e proteger informações confidenciais dentro da organização. Recentemente, a Contoso Ltd. notou atividades de navegação incomuns que podem expor dados confidenciais. Para lidar proativamente com esse risco interno, você implementará o Gerenciamento de Risco Interno do Microsoft Purview, concentrando-se em identificar, analisar e responder a possíveis ameaças internas de forma eficaz.

**Tarefas:**

1. Atribuir permissões de gerenciamento de risco interno
1. Configurar indicadores de risco interno
1. Criar uma política de risco interno
1. Personalizar a política de vazamentos de dados
1. Habilitar a integração do Microsoft Defender para Ponto de Extremidade ao Gerenciamento de Risco Interno
1. Habilitar indicadores e configurar usuários prioritários
1. Criar uma política para violações de política de segurança por usuários prioritários
1. Criar um modelo de aviso

## Tarefa 1 — Atribuir permissões de gerenciamento de risco interno

Nesta tarefa, você atribuirá a Joni Sherman a função Gerenciamento de Risco Interno para que ela possa acessar e gerenciar recursos de risco interno no Microsoft Purview.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin**.

1. No Microsoft Edge, navegue até **`https://purview.microsoft.com`** e entre no portal do Microsoft Purview como Administrador MOD, `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.

1. Selecione **Configurações** > **Funções e Escopos** > **Grupos de função**.

1. Na página **Grupos de função para Soluções do Microsoft Purview**, selecione **Gerenciamento de Risco Interno**.

1. No painel de submenu **Gerenciamento de Risco Interno** à direita, selecione **Editar**.

1. Na página **Editar membros do grupo de função**, selecione **+ Escolher usuários**.

1. No painel de submenu **Escolher usuários**, pesquise `Joni` e marque a caixa de seleção **Joni Sherman**.

1. Clique no botão **Selecionar** na parte inferior do painel.

1. Na página **Editar membros do grupo de função**, selecione **Avançar**.

1. Na página **Revisar o grupo de função e concluir**, selecione **Salvar**.

1. Depois de adicionar Joni ao grupo de função, selecione **Concluído** na página **Você atualizou o grupo de função**.

1. Saia da conta **Administrador MOD** clicando no ícone MA no canto superior direito da janela e, em seguida, em **Sair**.

Você atribuiu a Joni as permissões necessárias para trabalhar com o Gerenciamento de Risco Interno no portal do Microsoft Purview.

## Tarefa 2 — Configurar indicadores de risco interno

Antes de criar uma política de risco interno, você ativará os indicadores necessários para a detecção. Esses indicadores definem os tipos de atividade de risco que o sistema procurará.

1. No **Microsoft Edge**, navegue até **`https://purview.microsoft.com`** e entre no portal do Microsoft Purview como `JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é a sua ID de locatário exclusivo fornecido pelo provedor de hospedagem de laboratório).

1. Selecione **Configurações** > **Gerenciamento de Risco Interno**.

1. Selecione a guia à esquerda de **Indicadores de política**.

1. Na página **Indicadores de política**, expanda e selecione **Selecionar tudo** para habilitar todos os indicadores nestas categorias:

   - Indicadores do Office
   - Detecção de exfiltração cumulativa

1. Escolha **Salvar** na parte inferior da página.

Você habilitou os principais indicadores de política para que o sistema possa detectar ações confidenciais, como exfiltração de arquivos ou atividades arriscadas do Office.

## Tarefa 3 — Criar uma política de risco interno

Nesta tarefa, você criará uma política rápida de vazamentos de dados para detectar e responder automaticamente ao comportamento arriscado do usuário relacionado à exfiltração de dados. As políticas rápidas usam modelos internos e limites padrão para simplificar a configuração.

1. No Microsoft Purview, selecione **Soluções** > **Gerenciamento de Risco Interno** > **Políticas**.

1. Na página **Políticas**, selecione **Criar política** e selecione a **Política rápida**.

1. No submenu **Criar políticas rápidas**, selecione **Introdução** em **Vazamentos de dados**.

1. Revise as configurações para criar uma política de vazamento de dados rápida e selecione **Criar política**.

1. Na página **A política de vazamento de dados está sendo criada**, marque as caixas de seleção:

   - Envie-me um e-mail quando as políticas tiverem avisos não resolvidos
   - Envie-me um e-mail quando novos alertas de alta gravidade forem gerados

     Em seguida, selecione **Atualizar configurações de notificação**.

1. Na parte inferior da página **A política de vazamento de dados está sendo criada**, selecione **Concluído**.

Você criou uma política rápida para detectar possíveis vazamentos de dados usando as configurações padrão. Em seguida, você o personalizará para resolver o aviso de configuração.

## Tarefa 4 — Personalizar a política de vazamentos de dados

Algumas políticas de risco interno requerem indicadores adicionais para funcionar corretamente. Nesta tarefa, você modificará sua política para habilitar indicadores de sequência e deixar a política em estado íntegro.

Na página **Políticas** de **Gerenciamento de Risco Interno**, você notará que sua política de vazamento de dados tem uma recomendação.

1. Selecione a **Política rápida de vazamento de dados** que você acabou de criar.

1. Revise a recomendação na página de submenu da política. Você tem um aviso informando que há **Indicadores de gatilho de sequência necessários não selecionados**. Para resolver esse aviso, selecione **Editar política**.

1. Na página **Escolher um modelo de política**, selecione **Avançar**.

1. Na página **Nomear política**, clique em **Avançar**.

1. N apágina **Escolher usuários, grupos e escopos adaptáveis**, selecione **Avançar**.

1. Na página **Excluir usuários e grupos (opcional) (versão prévia),** selecione **Avançar**.

1. Na página **Decidir se deseja priorizar o conteúdo**, selecione **Avançar**

1. Na página **Escolher evento de gatilho para esta política**, examine **Selecionar quais sequências dispararão essa política** e exiba as informações de que **Algumas sequências requerem que indicadores específicos sejam ativados em "Configurações" antes de serem selecionadas abaixo.**

1. Selecione a opção **Ativar indicadores** para habilitar os indicadores de sequência necessários para essa política.

1. O vazamento de dados é principalmente uma política de risco interno de exfiltração dos dados. Na caixa de diálogo para habilitar os indicadores de sequência, selecione **Selecionar tudo** para ativar todos os **Indicadores de exfiltração** necessários e, em seguida, selecione **Salvar**.

1. Selecione **Avançar** na página **Escolher evento de gatilho para esta política**.

1. Na página **Escolher limites para eventos de gatilho**, selecione **Avançar**.

1. Na página **Indicadores**, selecione **Avançar**.

1. Na página **Opções de detecção**, selecione **Avançar**.

1. Na página **Escolher tipo de limite para indicadores**, selecione **Avançar**.

   Essa política usa um evento de gatilho e indicadores internos. Ela começa a avaliar a atividade do usuário somente quando Microsoft Defender para Ponto de Extremidade detecta ameaças como evasão de defesa ou software indesejado.

1. Na página **Examinar configurações e concluir**, selecione **Enviar**.

1. Na página **A política foi criada**, selecione **Concluído**.

1. De volta à página **Políticas**, a política agora terá o status **Íntegra**.

Sua política de risco interno agora está íntegra e pronta para detectar atividades arriscadas com base em gatilhos de sequência e indicadores habilitados.

## Tarefa 5 — Habilitar a integração do Microsoft Defender para Ponto de Extremidade ao Gerenciamento de Risco Interno

Nesta tarefa, você habilitará a integração entre o Microsoft Defender para Ponto de Extremidade e o Microsoft Purview para que os alertas de segurança possam ser usados em políticas de risco interno.

1. No Microsoft Edge, navegue até o Microsoft Defender acessando `https://security.microsoft.com`.

1. No painel de navegação esquerdo, selecione **Configurações** > **Pontos de extremidade** > **Recursos avançados**.

1. Role para baixo e selecione a alternância para **Ativado** para **Compartilhar pontos de extremidade com o Centro de Conformidade da Microsoft**.

   ![Captura de tela mostrando a opção Compartilhar pontos de extremidade com o Centro de Conformidade da Microsoft.](../Media/enable-irm-in-mde.png)

1. Na parte inferior da tela, selecione **Salvar preferências**.

Você habilitou o Defender para Ponto de Extremidade para compartilhar alertas com o Microsoft Purview.

## Tarefa 6 — Habilitar indicadores e configurar usuários prioritários

Nesta tarefa, você configurará os indicadores de política e criará um grupo de usuários prioritários que pode ser usado em políticas de risco interno.

1. No **Microsoft Edge**, navegue até `https://purview.microsoft.com`.

1. Selecione **Configurações** > **Gerenciamento de Risco Interno**.

1. Selecione a guia à esquerda de **Indicadores de política**.

1. Na página **Indicadores de política**, expanda e selecione **Selecionar tudo** para habilitar todos os indicadores nestas categorias:

   - Indicadores no Microsoft Defender para Ponto de Extremidade (prévia)
   - Indicadores de navegação arriscada (prévia)

1. Escolha **Salvar** na parte inferior da página.

1. Selecione a guia **Grupos de usuários prioritários** e, em seguida, **+ Criar grupo de usuários prioritário**.

1. Na página **Nome e descrição do grupo de usuários prioritário**, insira:

   - **Nome**: `Finance team`
   - **Descrição**: `Team members who manage financial operations, budgeting, and payroll systems.`

1. Selecione **Avançar**.

1. Na página **Membros**, selecione **+ Membros**.

1. No submenu **Membros**, pesquise e selecione:

   - `Lynne Robbins`
   - `Debra Berger`
   - `Megan Bowen`

1. Selecione **Adicionar** para adicionar os três membros ao grupo de prioridade da equipe de finanças.

1. Selecione **Avançar**.

1. Em **Escolher quem pode exibir dados envolvendo usuários neste grupo prioritário**, selecione **+ Escolher usuários e grupos de funções**.

1. No submenu, marque a caixa de seleção do **Gerenciamento de Risco Interno** e selecione **Adicionar**.

1. Selecione **Avançar**.

1. **Revise** e **Envie** suas configurações e selecione **Concluído** depois de criar o grupo de usuários prioritário.

Você configurou indicadores de política e criou um grupo prioritário para monitorar usuários de alto risco.

## Tarefa 7: criar uma política para violações da política de segurança por usuários prioritários

Nesta tarefa, você criará uma política de risco interno que detecta alertas do Defender para Ponto de Extremidade buscando atividades arriscadas por usuários prioritários.

1. No Microsoft Purview, selecione **Soluções** > **Gerenciamento de Risco Interno** > **Políticas**.

1. Na página **Políticas**, selecione **Criar política** e **Política personalizada**.

1. Na página **Escolher um modelo de política**, selecione **Violações da política de segurança por usuários prioritários (prévia)**. Em seguida, selecione Avançar.

1. Na página **Nomear política**, insira:

   - **Nome**: `Security policy violations - Priority users`
   - **Descrição**: `Detects Defender for Endpoint alerts for risky activity by priority users, such as malware or disabled protections.`

1. Selecione **Avançar**.

1. Na página **Escolher usuários, grupos e escopos adaptáveis**, selecione **Adicionar ou editar grupos de usuários prioritários**.

1. No submenu **Escolher grupos de usuários prioritários**, marque a caixa de seleção do grupo **Equipe financeira** e selecione Adicionar.

1. Selecione **Avançar**.

1. Na página **Decidir se deseja priorizar o conteúdo**, selecione **Avançar**.

1. Na página **Escolher evento de gatilho para esta política**, selecione **Avançar**.

1. Na página **Indicadores**, selecione **Avançar**.

1. Na página **Escolher tipo de limite para indicadores**, deixe a opção **Aplicar limites padrão fornecida pela Microsoft** marcada e selecione **Avançar**.

1. Na página **Examinar configurações e concluir**, selecione **Enviar**.

1. Na página **Sua política foi criada**, selecione **Concluído**.

Você criou uma política de risco interno personalizada que usa sinais do Defender para Ponto de Extremidade a fim de detectar atividades arriscadas de usuários prioritários.

## Tarefa 8: criar um modelo de aviso

Nesta tarefa, você criará um modelo de aviso no Microsoft Purview para notificar os usuários quando um alerta de risco interno for disparado.

1. No Microsoft Purview, selecione **Soluções** > **Gerenciamento de Risco Interno** > **Modelos de aviso**.

1. Na página **Modelos de aviso**, selecione **+ Criar modelo de aviso**.

1. Preencha as informações necessárias no painel de submenu **Criar um novo modelo de aviso** à direita.

    - **Nome do modelo:** `Security Violation Alert`
    - **Enviar de:** `Joni Sherman`
    - **Assunto**: `Unusual activity detected - please review`
    - **Corpo da mensagem:**

        ````html
        <!DOCTYPE html>
        <html>
        <body>
        <h2>Security Alert</h2>
        <p>We've detected activity from your account that might violate our organization's security policies. This could be due to malware, disabled protections, or other risky behavior.</p>
        <p>Please review your recent actions and ensure your device security settings are up to date. If you believe this alert was generated in error, contact the IT Security team for assistance.</p>
        <p>To avoid future issues, refer to the <a href="https://contoso.com/security-guidelines">Contoso Security Guidelines</a>.</p>
        <p>Thank you,</p>
        <p><em>Compliance and Security Team</em></p>
        </body>
        </html>
        ````

1. Selecione **Criar**.

1. N página **Modelos de aviso**, você verá o modelo de **Alerta de violação de segurança** que acabou de criar.

Você criou um modelo de aviso que o Gerenciamento de Risco Interno pode usar para notificar os usuários sobre violações da política de segurança.
