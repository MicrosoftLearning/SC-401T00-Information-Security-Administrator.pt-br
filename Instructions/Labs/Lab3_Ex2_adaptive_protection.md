---
lab:
  title: 'Exercício 2: implementar a proteção adaptável'
  module: Module 3 - Implement Insider Risk Management
---

# Laboratório 3 - Exercício 2: implementar a proteção adaptável

Você é Joni Sherman, administradora de segurança da informação da Contoso Ltd. Sua função envolve proteger dados confidenciais e responder a riscos internos. Para aprimorar a proteção, você habilitará a Proteção adaptável do Microsoft Purview, que ajusta dinamicamente a imposição da DLP (Prevenção Contra Perda de Dados) com base nos níveis de risco interno.

**Tarefas:**

1. Atribuir uma política de risco interno à Proteção adaptável
1. Definir configurações de proteção adaptável para sua política DLP
1. (Opcional) Configurar o acesso condicional com proteção adaptável
1. Ativar a proteção adaptável

## Tarefa 1: atribuir uma política de risco interno à Proteção adaptável

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin**.

1. No **Microsoft Edge**, vá até **`https://purview.microsoft.com`** e entre como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem de laboratório).

1. No portal do Microsoft Purview, vá até **Soluções** > **Gerenciamento de risco interno** > **Proteção adaptável**.

1. No painel de navegação esquerdo, selecione **Níveis de risco interno**.

1. Na página **Níveis de risco interno**:

   - Na lista suspensa Política de risco interno, selecione a **Política rápida de vazamentos de dados** que você criou em um exercício anterior.
   - Mantenha as configurações padrão de nível de risco inalteradas.
   - Selecione **Salvar**.

Você vinculou uma política de risco interno à Proteção adaptável, permitindo ações dinâmicas com base em risco no Microsoft Purview.

## Tarefa 2: definir configurações de proteção adaptável para sua política DLP

Agora que a Proteção adaptável está vinculada à sua política de risco interno, você atualizará uma política DLP para responder a níveis de risco elevados bloqueando o compartilhamento de dados confidenciais.

1. No Microsoft Purview, vá até **Soluções** > **Prevenção da perda de dados** > **Políticas**.

1. Na página **Políticas**, marque a caixa de seleção da política **DLP - Proteção de Cartão de Crédito** criada em um exercício anterior e selecione **Editar política**.

1. Na configuração DLP, selecione **Avançar** até chegar à página **Personalizar regras avançadas de DLP**.

1. Selecione o ícone de lápis ao lado da **Regra de informações do cartão de crédito** para editá-la.

1. Na página **Editar regra**:
   - No campo **Descrição**, insira: `Block sharing of credit card data when user has an elevated insider risk level.`
   - Na seção **Condições**, selecione **Adicionar condição** > **Nível de risco interno para Proteção adaptável é**.
   - Na nova seção, selecione **Risco elevado**.
   - Em **Ações**, defina **Restringir acesso ou criptografar o conteúdo no Microsoft 365** como **Bloquear todos**.
   - Selecione **Salvar** para atualizar a regra.

1. De volta à página **Personalizar regras avançadas de DLP**, selecione **Avançar**.

1. Na página **Modo de política**, mantenha a política ativa e selecione **Avançar**.

1. Na página **Revisar e concluir**, selecione **Enviar** e, em seguida, **Concluído** quando a política for atualizada.

Você atualizou sua política DLP para bloquear o compartilhamento quando o risco interno é elevado, fortalecendo a proteção de dados com base no comportamento do usuário.

## Tarefa 3: (opcional) configurar o acesso condicional com proteção adaptável

Para adicionar outra camada de imposição, você pode usar níveis de risco interno para restringir o acesso usando o Acesso condicional. Nesta tarefa, você criará uma política que bloqueia o acesso de usuários com um nível elevado de risco interno.

1. No Microsoft Purview, saia da conta de Joni e feche todas as janelas do navegador.

1. Abra o Microsoft Edge e vá até o **centro de administração do Microsoft Entra** em `https://entra.microsoft.com`. Entre como **Administrador MOD**, `admin@WWLxZZZZZZ.onmicrosoft.com` (em que ZZZZZZ é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha de Administrador deve ser fornecida pelo seu provedor de hospedagem do laboratório.

1. Na página **Requer mais informações**, selecione **Avançar**.

1. Na página **Manter sua conta segura**, siga as instruções para configurar a MFA (autenticação multifator) usando o Microsoft Authenticator ou outro app de autenticação.

   Depois de concluir a configuração da MFA, você voltará para o **centro de administração do Microsoft Entra**.

1. No Centro de administração do Microsoft Entra, vá até **Proteção** > **Acesso condicional** > **Políticas**.

1. Na página **Políticas**, selecione **+ Nova política**.

1. Na página **Nova política**, nomeie sua política: `Block all access for elevated risk`.

1. Em **Atribuições**, configure a seção **Usuários**:

   - **Incluir**: todos os usuários  
   - **Excluir**: `Joni Sherman`e `MOD Administrator`

     ![Captura de tela mostrando onde excluir usuários no Acesso Condicional.](../Media/ca-exclude-users.png)

1. Em **Recursos de destino**, confirme se a lista suspensa está definida como **Recursos (anteriormente aplicativos na nuvem)** e selecione **Todos os recursos (anteriormente 'Todos os aplicativos na nuvem')**.

     ![Captura de tela mostrando como configurar recursos de destino no Acesso Condicional.](../Media/ca-target-resources.png)

1. Em **Condições**, selecione **Risco interno**. Defina **Configurar** como **Sim** e, em seguida, defina o nível de risco como **Elevado**.

     ![Captura de tela mostrando a configuração de risco interno no Acesso Condicional.](../Media/ca-insider-risk-levels.png)

1. Em **Controles de acesso**, selecione **Conceder**. Escolha **Bloquear acesso** e selecione **Selecionar** na parte inferior do submenu.

     ![Captura de tela mostrando onde bloquear o acesso no Acesso Condicional.](../Media/ca-block-access.png)

1. Na parte inferior da página, confirme se **Habilitar política** está definido como **Somente relatório** e selecione **Criar**.

1. De volta à página **Políticas** para Acesso Condicional, selecione **Atualizar** para verificar se a política recém-criada aparece.

1. Saia da conta do Administrador Mod selecionando o ícone MA no canto superior direito da janela, selecionando **Sair** e fechando todas as janelas do navegador.

Você criou uma política de Acesso Condicional que bloqueia o acesso de usuários de risco elevado, sem afetar o acesso imediatamente, pois a política está no modo somente relatório.

## Tarefa 4 - Habilitar a Proteção adaptável

Nesta tarefa final, você ativará a Proteção adaptável para que o sistema possa começar a aplicar a imposição dinâmica com base no risco interno.

1. Abra o **Microsoft Edge** e navegue até **`https://purview.microsoft.com`** e faça login como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (onde ZZZZZZ é o sua ID de locatário exclusiva fornecido pelo provedor de hospedagem do seu laboratório).

1. Navegue até **Soluções** > **Gerenciamento de riscos internos** > **Proteção adaptável**.

1. Confirme suas configurações:

   - Na guia **Níveis de risco interno**, a **Política rápida contra vazamento de dados** está selecionada.

   - Na guia **Acesso condicional**, a política **Bloquear todo o acesso para risco elevado** fica visível (opcional).

   - Na guia **Prevenção contra perda de dados**, a política **DLP - Proteção de cartão de crédito** é listada.

1. Selecione a guia **Configurações de proteção adaptável**.

1. Alterne **Proteção adaptável** para **Ativada** e selecione **Salvar**.

Você ativou a Proteção adaptável com sucesso. As ações de imposição agora serão ajustadas automaticamente com base no nível de risco interno de um usuário.
