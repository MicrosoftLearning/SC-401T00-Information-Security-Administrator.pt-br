---
lab:
  title: Exercício 2 - Implementar e gerenciar DLP de ponto de extremidade
  module: Module 2 - Implement Data Loss Prevention
---

# Laboratório 2 - Exercício 2 - Implementar e gerenciar DLP de ponto de extremidade

Joni Sherman, a recém-contratada Administradora de Segurança da Informação da Contoso Ltd., foi solicitada a fortalecer os controles DLP nos dispositivos da empresa. Alguns funcionários têm copiado informações confidenciais de clientes para unidades USB, aumentando o risco de exposição de dados. Neste laboratório, Joni configurará uma política DLP de ponto de extremidade para bloquear essas transferências.

**Tarefas:**

1. Integrar um dispositivo para DLP de ponto de extremidade
1. Criar uma política DLP de ponto de extremidade
1. Definir configurações de DLP do Ponto de Extremidade
1. Configurar a extensão do Microsoft Purview

## Tarefa 1 - Integrar um dispositivo para DLP de ponto de extremidade

Nesta tarefa, você integrará um dispositivo Windows 11 para que ele esteja pronto para ser protegido por políticas DLP de ponto de extremidade.

1. Faça login em **VM do Cliente 2 (SC-401-CL2)** como a conta **SC-401-cl1\admin**.

1. Abra o Microsoft Edge, navegue até**`https://purview.microsoft.com`** e faça login no portal do Microsoft Purview como **Joni Sherman**. Entre como `JoniS@WWLxZZZZZZ.onmicrosoft.com`, (em que zzzzzz é a sua ID de locatário exclusiva fornecida pelo seu provedor de hospedagem de laboratório). A senha de Joni foi definida em um exercício anterior.

1. Selecione **Configurações** na barra lateral esquerda.

1. Na barra lateral esquerda, expanda **Integração de dispositivos** e selecione **Integração**.

1. Na página **Integração**, no menu suspenso **Método de implantação**, selecione **Script local (para até 10 máquinas)** e selecione **Baixar pacote**.

1. Na caixa de diálogo **Downloads**, passe o cursor sobre o download e selecione o ícone da pasta para **Mostrar na pasta**.

1. Extraia o arquivo zip para a **área de trabalho** do SC-401-CL1. Você deve ver um script chamado **DeviceComplianceLocalOnboardingScript.cmd**.

1. Na área de trabalho, clique com o botão direito do mouse no arquivo **DeviceComplianceLocalOnboardingScript.cmd** que você acabou de extrair e selecione **Mostrar mais opções**, depois selecione **Propriedades**.

1. Na parte inferior da guia **Geral** da janela de propriedades, na seção **Segurança**, selecione **Desbloquear** e, em seguida, selecione **OK** para salvar essa configuração.

1. De volta à área de trabalho, clique com o botão direito do mouse em **DeviceComplianceLocalOnboardingScript.cmd** e selecione **Executar como administrador**. Na caixa de diálogo **Controle de Conta de Usuário**, selecione **Sim**.

1. Na tela **Prompt de comando**, digite **Y** para confirmar e pressione Enter.

1. Quando o script estiver concluído, você receberá uma mensagem de sucesso e uma solicitação para **Pressionar qualquer tecla para continuar**. Pressione qualquer tecla para fechar a janela da linha de comando. A integração pode demorar um minuto.

1. Abra o menu Iniciar e procure por `Access work or school`. Selecione **Acessar trabalho ou escola** em **Melhor correspondência**.

1. Na janela **Acessar trabalho ou escola** para **Adicionar uma conta corporativa ou de estudante**, selecione **Conectar**.

1. Na caixa de diálogo **Configurar uma conta corporativa ou de estudante**, selecione o link **Associar este dispositivo ao Microsoft Entra ID** e faça login como **Joni Sherman**`JoniS@WWLxZZZZZZ.onmicrosoft.com` (onde ZZZZZZ é sua ID de locatário exclusiva fornecida pelo provedor de hospedagem do laboratório). A senha de Joni foi definida em um exercício anterior.

1. Na caixa de diálogo **Verifique se esta é a sua organização**, verifique o URL do locatário e selecione **Ingressar**.  

1. Quando o dispositivo estiver conectado, selecione **Concluído** em **Tudo pronto!** tela.

1. Reinicie a VM do cliente 2 (SC-401-CL2).

1. Faça logon novamente na VM do Cliente 1 (SC-401-CL1).

1. A janela Microsoft Purview ainda deve estar aberta na página **Dispositivos**. Atualize esta página e verifique se o dispositivo foi integrado com êxito.

Você integrou o dispositivo com sucesso e o inscreveu no Microsoft Entra ID. Agora ele pode ser protegido por políticas DLP de ponto de extremidade.

## Tarefa 2 - Criar uma política DLP de ponto de extremidade

Nesta tarefa, você criará uma política DLP que bloqueia a transferência de informações confidenciais para unidades USB. Isso ajuda a reduzir o risco de os dados serem retirados do local sem autorização.

1. Entre na VM do Cliente 1 (SC-401-CL1) como a conta SC-401-cl1\admin.

1. Você ainda deve estar na página **Dispositivos** no portal do Microsoft Purview, conectado como Joni Sherman.

1. No portal do Microsoft Purview, selecione **Soluções** > **Prevenção contra perda de dados**.

1. No painel de navegação à esquerda, selecione **Políticas** e **+ Criar política**.

1. Na página **Iniciar com um modelo ou criar uma política personalizada**, escolha **Personalizada**, **Política personalizada** e **Avançar**.

1. Na página **Nomear a sua política de DLP**, insira:

    - **Nome**: `Block USB transfers`
    - **Descrição**: `Prevent transferring sensitive data to USB devices.`

1. Na página **Atribuir unidades administrativas**, clique em **Avançar**.

1. Na página **Escolher locais para aplicar a política**, verifique se apenas o local **Dispositivos** está selecionado. Se qualquer outro local estiver selecionado, verifique se ele está desmarcado e selecione **Avançar**.

1. Na página **Definir configurações de política**, selecione **Criar ou personalizar regras DLP avançadas** e selecione **Avançar**.

1. Na página **Personalizar regras avançadas de DLP**, escolha **+ Criar regra**.

1. Na página **Criar regra**, insira:

    - **Nome**: `USB transfer rule`
    - **Descrição**: `Block USB transfers of sensitive data.`

1. Em **Condições**, selecione **+ Adicionar condição** e **O conteúdo contém**.

1. Na nova seção **Conteúdo contém**:
    - Selecione **Adicionar** > **Tipos de informações confidenciais**.
    - Na página **Tipos de informações confidenciais**, pesquise estes tipos de informações confidenciais:
       - `Credit Card Number`
       - `U.S. Social Security Number (SSN)`
       - `U.S. Driver's License Number`
       - `Contoso Employee IDs`

1. Em **Ações**, selecione **+ Adicionar uma ação** > **Auditar ou restringir atividades em dispositivos**.

1. Na nova seção **Auditar ou restringir atividades em dispositivos**:
    - Na seção **Atividades de arquivo para todos os aplicativos**, certifique-se de que **Copiar para um dispositivo USB removível** esteja selecionado.
    - Selecione a lista suspensa à esquerda de **Copiar para um dispositivo USB removível** para alterar a ação de **Somente auditoria** para **Bloquear**.

1. Em **Notificações do usuário**:
    - **Ative** a alternância **Usar as notificações para informar os usuários e ajudar a instruí-los sobre o uso adequado de informações confidenciais**.
    - Marque a caixa de seleção para **Exibir aos usuários uma notificação de dica de política quando uma atividade for restringida**.

1. Selecione **Salvar** na parte inferior do submenu **Criar regra**.

1. De volta à página **Personalizar regras avançadas de DLP**, clique em **Avançar**.

1. Na página **Modo de política**, selecione **Executar a política no modo de simulação**.
   - Marque a caixa de seleção para **Exibir dicas de política enquanto estiver no modo de simulação**.
   - Além disso, marque a caixa de seleção para **Ativar a política se ela não for editada dentro de quinze dias após a simulação**.

1. Selecione **Avançar**.

1. Na página **Revisar e concluir**, revise as configurações da política e clique em **Enviar** para criar a política.

1. Depois que a política for criada, selecione **Concluído** na página **Nova política criada**.

Você criou uma política DLP no modo de simulação que bloqueia transferências USB de dados confidenciais. Se a política não for editada, ela será ativada automaticamente após 15 dias.

## Tarefa 3 — Definir as configurações de DLP do ponto de extremidade

Nesta tarefa, você ajustará as configurações de DLP do ponto de extremidade excluindo uma pasta local, definindo restrições do navegador e bloqueando um domínio de nuvem.

1. Você ainda deve estar na VM do Cliente 1 (SC-401-CL1) como a conta **SC-401-cl1\admin** e no Microsoft 365 como **Joni Sherman**.

1. No Microsoft Purview, no painel de navegação à esquerda, selecione **Configurações** > **Prevenção contra perda de dados**.

1. A página **Configurações de Prevenção contra perda de dados** abrirá nas **Configurações de DLP de ponto de extremidade**.

1. Na página **Configurações de DLP de ponto de extremidade**, expanda **Exclusões de caminho de arquivo para Windows** e selecione **+ Adicionar exclusão de caminho de arquivo**.

1. Na página de submenu **Excluir estes caminhos de arquivo de dispositivos Windows**, no campo **Exclusão de caminho de arquivo**, digite `C:\FilePathExclusionTest` e clique no botão **+** à direita. Selecione **Salvar** para salvar essa entrada.

1. De volta à página **Configurações de DLP de ponto de extremidade**, expanda **Restrições de navegador e domínio para dados confidenciais** e selecione **+ Adicionar ou editar navegadores não permitidos**.

1. Na página de submenu **Adicionar navegadores não permitidos**, marque a caixa de seleção **Google Chrome** e selecione **Salvar**.

1. De volta à página de **Configurações de DLP do ponto de extremidade**, selecione a lista suspensa em **Domínios de serviço** e altere-a de **Desativado** para **Bloquear**.

1. Na caixa de diálogo **Atualizar modo de aplicativo de nuvem**, selecione **Sim** para ativar o modo de bloqueio.

1. Em **Domínios de serviço**, selecione **+ Adicionar domínio de serviço de nuvem**.

1. Na página de submenu **Adicionar domínio de serviço de nuvem**, no campo **Domínio**, digite `dropbox.com` e clique no ícone **+** (mais) para adicionar o caminho. Selecione **Salvar** para salvar essa configuração.

Você aplicou configurações personalizadas de ponto de extremidade que refinam o comportamento de sua política, incluindo exclusões, restrições de navegador e bloqueio de acesso a domínios específicos.

## Tarefa 4: configurar a extensão do Microsoft Purview

Nesta tarefa, você instalará a Extensão do Microsoft Purview no Google Chrome para testar o comportamento da política DLP do ponto de extremidade em navegadores compatíveis.

1. Abra o navegador Edge na barra de tarefas.

1. Vá até o download do Google Chrome em **`https://chrome.google.com`**.

1. Selecione **Baixar Chrome** e **Abrir arquivo** na notificação de **Downloads** para **ChromeSetup.exe**.

1. Selecione **Sim** na caixa de diálogo **Controle de Conta de Usuário** para instalar o navegador Chrome.

1. Quando a instalação for concluída, na tela **Fazer login no Chrome**, selecione **Não, obrigado** ou **Não entrar**.

1. Selecione **Ignorar** na página **Definir seu navegador padrão**.

1. Quando a janela do navegador Chrome recém-instalada for aberta, vá até a **Extensão do Microsoft Purview** na **Chrome Web Store** em:

   `https://chrome.google.com/webstore/detail/microsoft-purview-extensi/echcggldkblhodogklpincgchnpgcdco`

1. Confirme se você está na página de extensão correta e selecione **Adicionar ao Chrome**.

1. Na janela **Adicionar "Extensão do Microsoft Purview"?** , selecione **Adicionar extensão**.

1. Feche a notificação da extensão que está sendo adicionada ao Chrome e vá até **`chrome://extensions`**.

1. Valide se a **Extensão do Microsoft Purview** está visível e ativada.

1. Feche a janela do navegador Chrome.

Você instalou o Chrome com êxito e adicionou a Extensão do Microsoft Purview. O dispositivo agora oferece suporte à aplicação de políticas DLP no Edge e no Chrome.
