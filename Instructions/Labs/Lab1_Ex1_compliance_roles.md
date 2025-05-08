---
lab:
  title: Exercício 1 — Gerenciar funções de conformidade e segurança
  module: Module 1 - Implement Information Protection
---
## Locatários do WWL – Termos de uso

Se você estiver recebendo um locatário como parte de uma entrega de treinamento com instrutor, observe que o locatário é disponibilizado com a finalidade de dar suporte aos laboratórios práticos no treinamento com instrutor.

Os locatários não devem ser compartilhados ou usados para fins fora dos laboratórios práticos. O locatário usado neste curso é um locatário de avaliação e não pode ser usado ou acessado após o fim da aula e não está qualificado para extensão.

Os locatários não podem ser convertidos em uma assinatura paga. Os locatários obtidos como parte deste curso permanecem a propriedade da Microsoft Corporation e reservamos o direito de obter acesso e a qualquer momento.

# Laboratório 1 — Exercício 1 — Gerenciar funções de conformidade e segurança

Como o Administrador de Segurança da Informação recém-contratada para a Contoso Ltd., você (Joni Sherman) precisa garantir que o novo locatário do Microsoft 365 esteja em conformidade com vários padrões legais e regulatórios. A Contoso Ltd. está se expandindo e a sua função é crucial para manter a conformidade em suas regiões.

**Tarefas:**

1. Atribuir funções de conformidade e segurança
1. Explorar o portal do Microsoft Purview

## Tarefa 1 — Atribuir funções de conformidade e segurança

Nesta tarefa, você atribuirá a função de Administrador de Conformidade a Joni Sherman.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**. A senha deve ser fornecida pelo seu provedor de hospedagem de laboratório.

1. Abra o **Microsoft Edge** e navegue até o centro de administração do Microsoft 365, `https://admin.microsoft.com`, e entre como **Administrador MOD**, `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é a ID de locatário exclusiva fornecido pelo provedor de hospedagem de laboratório). A senha de administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.

1. Na barra lateral esquerda, expanda **Usuários** e selecione **Usuários ativos**.

1. Na página **Usuários ativos**, pesquise `Joni` e selecione **Joni Sherman**.

1. As propriedades da conta de Joni serão exibidas em um painel de submenu à direita. Selecione **Gerenciar funções** no painel de submenu.

1. No painel **Gerenciar funções de administrador**, selecione **Acesso ao centro de administração** e role para baixo para expandir **Exibir tudo por categoria**.

1. Na categoria **Segurança e conformidade**, marque a caixa de seleção **Administrador de conformidade** e **Administrador de segurança** e, em seguida, selecione **Salvar alterações** na parte inferior do painel de submenu.

1. Você verá uma mensagem: **Funções de administrador atualizadas**.

1. Na página **Gerenciar funções de administrador**, clique no **X** no canto superior direito do painel de submenu para fechar o painel.

1. Saia da conta de Administrador MOD clicando no ícone **MA** no canto superior direito e, em seguida, em **Sair**.

   ![Captura de tela mostrando o caminho de navegação para sair da conta de administrador do MOD.](../Media/sign-out.png)

Você atribuiu a Joni Sherman as funções de Administrador de Conformidade e Segurança, que são necessárias para concluir as tarefas neste laboratório.

## Tarefa 2 — Explorar o portal do Microsoft Purview

Nesta tarefa, você entrará como Joni Sherman para explorar o portal do Microsoft Purview.

1. Você ainda estará na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-CL1\admin**.

1. No **Microsoft Edge**, navegue até **`https://purview.microsoft.com`**.

1. Quando a janela **Escolher uma conta** for exibida, escolha **Usar outra conta**.

1. Quando a janela **Entrar** for exibida, entre como `JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. Uma mensagem sobre o novo portal do Microsoft Purview aparecerá na tela. Selecione **Introdução** para acessar o novo portal.

    ![Captura de tela mostrando a tela de Boas-vindas ao novo porta do Microsoft Purview.](../Media/welcome-purview-portal.png)

1. Familiarize-se com o novo portal do Microsoft Purview. Quando terminar, deixe a janela do navegador aberta.

Você alternou para a conta de Joni Sherman e agora já pode iniciar o laboratório.
