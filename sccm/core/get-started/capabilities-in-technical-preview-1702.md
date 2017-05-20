---
title: "Capacidades na pré-visualização técnica 1702 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1702."
ms.custom: na
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 8f4ec982a54cf3cefef310268a54850e70e2e63a
ms.openlocfilehash: 3bdbcd1a3c64a1d50f2f6219b2a5e17d60979864
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1702 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1702. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

Esta pré-visualização apresenta novas opções de comentários na consola do Configuration Manager. As opções de comentários permite-lhe enviar comentários diretamente para a equipa de desenvolvimento, a título de Web site do Configuration Manager UserVoice comentários.  

>Pode encontrar o **comentários** opção:
-  No Friso, na extremidade esquerda do separador de cada nó.  
   ![Friso](./media/feedback-home.png)

-  Quando lhe com o botão direito em qualquer objeto na consola.   
    ![Opção de clique Righ](./media/feedback-option.png)   

Escolher **comentários** abre-se o browser para o Configuration Manager UserVoice comentários Web site, em https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Alterações à atualizações e manutenção
O seguinte é introduzido com esta pré-visualização.

**Opções de atualização mais simples**  
Da próxima vez que a infraestrutura são considerados para duas ou mais atualizações, apenas a atualização mais recente é transferida. Por exemplo, se a versão atual do site é dois ou mais mais antiga do que a versão mais recente está disponível, apenas essa versão de atualização mais recente é transferido automaticamente.  

Tem a opção para transferir e instalar outras atualizações disponíveis, mesmo quando não estiverem a versão mais atual. No entanto, irá receber um aviso de que a atualização foi substituída por uma mais recente. Para transferir uma atualização que seja *disponível para transferência*, selecione a atualização na consola e, em seguida, clique em **transferir**.

**Limpeza melhorada de atualizações anteriores**   
Adicionámos uma função de limpeza automática que elimina as transferências desnecessários da pasta 'EasySetupPayload' no servidor do site.  


## <a name="peer-cache-improvements"></a>Melhoramentos de Cache ponto a ponto
Começando com esta versão, um computador de origem de cache ponto a ponto irão rejeitar um pedido de conteúdo quando o computador de origem de cache ponto a ponto cumpra qualquer um dos seguintes condições:  
 -     Está no modo de bateria baixo.
 -  Carga de CPU excede 80% o momento que o conteúdo de exemplos é solicitado.
 -  E/s de disco tem um *AvgDiskQueueLength* que excede 10.
 -  Não existem ligações não mais disponíveis para o computador.   

Pode configurar estas definições utilizando a classe de configuração do agente de cliente para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) ao utilizar o SDK do System Center Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que efetuou irão continuar a atingir origens alternativas do formulário de conteúdo no seu agrupamento das localizações de origem de conteúdo disponível.   

## <a name="azurediscovery"></a>Utilizar o Azure Active Directory Domain Services para gerir dispositivos, utilizadores e grupos

Com esta pré-visualização técnica versão que pode gerir dispositivos que estão associados a um serviços de domínio do Azure Active Directory (AD) geridos domínio. Também pode detetar dispositivos, utilizadores e grupos nesse domínio com vários métodos de deteção do Configuration Manager.

A infraestrutura de site de pré-visualização técnica, clientes e o domínio de serviços de domínio do Azure AD tem de executar todos no Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurar o Gestor de configuração para utilizar o Azure AD
Para utilizar o Azure AD com o Configuration Manager, terá o seguinte:
-    Subscrição do Azure.
-    Azure AD com serviços de domínio (DS).
-    Um site do Configuration Manager que é executado com uma VM do Azure que esteja associado ao seu Azure AD.
-    Clientes do Configuration Manager que são executadas no mesmo ambiente do Azure AD.

Para configurar o serviço de domínio do Azure AD, consulte o artigo [começar com os serviços de domínio do Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### <a name="discover-resources"></a>Detetar recursos
Depois de configurar o Gestor de configuração para ser executado no Azure AD, pode utilizar os seguintes métodos de deteção do Active Directory para procurar o Azure AD para recursos:  
- Deteção de Sistemas do Active Directory
- Deteção de Utilizadores do Active Directory
- Deteção de Grupos do Active Directory  

Para cada método utilizado, edite a consulta LDAP para pesquisar as estruturas do Azure AD UO em vez dos contentores são característicos ao Active Directory no local. Isto requer direcionar a consulta para pesquisar o Active Directory na sua subscrição do Azure.  

Os exemplos seguintes utilizam um Azure AD de *contoso.onmicrosoft.com*:
 - **Deteção de sistemas**   
Azure AD armazena dispositivos sob o **AADDC computadores** UO.  Configure o seguinte:  
  -    *LDAP://ou=AADDC computadores, DC = contoso, DC = onmicrosoft, DC = com*  


- **Deteção de utilizadores** AAD armazena utilizadores sob o **AADDC utilizadores** UO.  Configure o seguinte:
  - *Os utilizadores LDAP://ou=AADDC, DC = contoso, DC = onmicrosoft, DC = com*


- **Deteção de grupos**  
Azure AD não tem um UO que armazena grupos. Em vez disso, utilize a mesma estrutura geral como as consultas de sistema ou o utilizador e configurar a consulta LDAP para apontar para a UO que contém os grupos que pretende detetar.

Consulte o seguinte para obter mais informações sobre o Azure AD:  
 - [Serviços de domínio do Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory-ds) no azure.microsoft.com.
 - [Documentação dos serviços de domínio do Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services) no docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Melhoramentos de política de conformidade de dispositivos de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para ajudar a bloquear o acesso aos recursos empresariais que suportam o acesso condicional, quando os utilizadores estão a utilizar as aplicações que fazem parte de uma lista de aplicações não conformes. A lista de aplicações não conformes pode ser definida pelo administrador quando adicionar a nova regra compatível **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir o **nome da aplicação**, a **ID da aplicação**e o **App Publisher** (opcional) quando adicionar uma aplicação à lista de não conformidade. Esta definição só se aplica a dispositivos iOS e Android.

Além disso, esta ajuda as organizações a mitigar fuga de dados através de aplicações não segura e a prevenir consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivos](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### <a name="try-it-out"></a>Experimente

**Cenário:** Identificar aplicações que estão a causar fuga de dados através do envio de dados da empresa fora da sua empresa ou que estão a causar consumo excessivo de dados, em seguida, [criar uma política de conformidade do dispositivo de acesso condicional](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) estas aplicações que adiciona a lista de aplicações não conformes. Isto irá bloquear o acesso aos recursos empresariais que suportam o acesso condicional até que o utilizador pode remover a aplicação bloqueada.

## <a name="antimalware-client-version-alert"></a>Alerta de versão do cliente de proteção contra software maligno
Iniciar com esta versão de pré-visualização, Configuration Manager Endpoint Protection oferece um alerta se mais de 20% (predefinição) dos clientes geridos estiver a utilizar uma versão do cliente de proteção contra software maligno (ou seja, o cliente do Windows Defender ou o Endpoint Protection) expirada.

### <a name="try-it-out"></a>Experimente
Certifique-se de que o Endpoint Protection está ativado em todos os clientes de ambiente de trabalho e o servidor através da política de definições de cliente. Agora pode ver **versão de cliente de proteção contra software maligno** e **estado de implementação do Endpoint Protection** acedendo **ativos e compatibilidade** > **descrição geral** > **dispositivos** > **todos os computadores de secretária e servir os clientes**. Para verificar a existência de um alerta, ver **alertas** no **monitorização** área de trabalho. Se mais de 20% dos clientes geridos estiver a executar uma versão expirada do software de proteção contra software maligno, a versão de cliente de proteção contra software maligno é desatualizada é apresentado o alerta. Este alerta não aparece no **monitorização** > **descrição geral** separador. Para atualizar clientes antimalware expirada, ative atualizações de software para clientes de proteção contra software maligno.

Para configurar a percentagem com que é gerado o alerta, expanda **monitorização** > **alertas** > **todos os alertas**, faça duplo clique **clientes de proteção contra software maligno desatualizados** e modificar o **emitir um alerta se a percentagem de clientes geridos com uma versão desatualizada do cliente de proteção contra software maligno é mais do que** opção.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Avaliação de compatibilidade para o Windows Update para atualizações de negócio
Agora pode configurar uma regra de atualização de política de conformidade para incluir uma atualização do Windows para o resultado da avaliação de negócio como parte da avaliação de acesso condicional.
> [!IMPORTANT]
> Tem de ter o Windows 10 Insider pré-visualização compilação 15019 ou posterior para utilizar a avaliação de compatibilidade para o Windows Update para atualizações de negócio.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir que o Windows Update para empresas gerir atualizações do Windows 10
Para recolher informações de avaliação de compatibilidade para Windows Update para atualizações de negócio, utilize o procedimento seguinte para configurar o agente de cliente para permitir explicitamente o Windows Update para empresas gerir atualizações do Windows 10.
1. Na consola do Configuration Manager, aceda a **Administração** > **Definições do Cliente**.
2. Nas propriedades para as definições de cliente, aceda a **atualizações de Software**e selecione **Sim** para o **gerir o Windows 10 atualizações com o Windows Update para empresas** definição.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Criar uma política de conformidade para o Windows Update para avaliação de negócio
1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **definições de compatibilidade** > **políticas de conformidade**.
2. Clique em **criar política de conformidade** ou selecione uma política de conformidade existente para modificar.
3. Na página geral, forneça um nome e uma descrição, selecione **regras de compatibilidade para dispositivos geridos com o cliente do Configuration Manager**, defina a gravidade de incompatibilidade para relatórios e clique em **seguinte**.
4. Na página de plataformas suportadas, selecione **Windows 10**e, em seguida, clique em **seguinte**.
5. Na página de regras, clique em **novo...** e, em seguida, para **condição** escolher **requerem o Windows Update para compatibilidade de empresas**. O **valor** definição é automaticamente definida para **verdadeiro**.

A nova política é apresentada no nó **Políticas de Conformidade** da área de trabalho **Ativos e Compatibilidade** .

### <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade
1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **definições de compatibilidade**e, em seguida, clique em **políticas de conformidade**.
2. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.
3. Na caixa de diálogo **Implemente a Política de Conformidade** , clique em **Procurar** para selecionar a coleção de utilizadores na qual a política será implementada.
   Além disso, pode selecionar opções de geração de alertas quando a política não está em conformidade, bem como configurar a agenda com base na qual a política será avaliada em termos de conformidade.
4. Quando tiver terminado, clique em **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade
Depois de criar a política de conformidade, pode monitorizar os resultados de compatibilidade na consola do Configuration Manager. Para obter mais detalhes, consulte o artigo [monitorizar a política de conformidade](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Foram introduzidos melhoramentos nas definições do Centro de Software e mensagens de notificação para sequências de tarefas de impacto elevado
Esta versão inclui as seguintes melhorias de mensagens de notificação para sequências de tarefas de implementação de impacto elevado e definições do Centro de Software:

- Nas propriedades para a sequência de tarefas, agora pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas não pertencente ao sistema operativo, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpre determinadas condições é automaticamente definida como impacto elevado. Para obter mais detalhes, consulte o artigo [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades para a sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou crie a sua própria mensagem de notificação personalizada para implementações de impacto elevado.
- Nas propriedades para a sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem tornar um reinício obrigatório, o tamanho de transferência da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de impacto elevado predefinida para direta atualiza agora os Estados que suas definições, aplicações e dados são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicado que todas as aplicações, dados e definições, seria perdidas, que não era aplica-se uma atualização no local.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de impacto elevado
Utilize o procedimento seguinte para definir uma sequência de tarefas como de impacto elevado.
> [!NOTE]
> Qualquer sequência de tarefas que cumpre determinadas condições é automaticamente definida como impacto elevado. Para obter mais detalhes, consulte o artigo [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **esta é uma sequência de tarefas de impacto elevado**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação personalizada para implementações de alto risco
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **utilizar texto personalizado**.
>  [!NOTE]
>  Só é possível definir o texto de notificação do utilizador quando o **esta é uma sequência de tarefas de impacto elevado** está selecionada.

4. Configure as seguintes definições (máximo de 255 carateres para cada caixa de texto):

   **Texto do título de notificação de utilizador**: Especifica o texto azul que apresenta a notificação de utilizador do Centro de Software. Por exemplo, a notificação do utilizador predefinição, esta secção contém algo como "A confirmar que pretende atualizar o sistema operativo neste computador".

   **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornece o corpo da notificação personalizada.
   - caixa de texto 1º: Especifica o corpo principal do texto, normalmente, que contém instruções para o utilizador. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "atualizar o sistema operativo demorará e o computador poderá reiniciar várias vezes."
   - caixa de texto 2º: Especifica o texto a negrito sob o corpo principal do texto. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "esta atualização no local instala o novo sistema operativo e automaticamente migrada suas definições, aplicações e dados."
   - caixa de texto do 3º: Especifica a última linha do texto sob o texto a negrito. Por exemplo, na notificação de utilizador predefinidas, esta secção contém algo como "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   

   Imaginemos que configura a seguinte notificação personalizada nas propriedades.

   ![Notificação personalizada para uma sequência de tarefas](.\media\user-notification.png)

   Será apresentada a seguinte mensagem de notificação quando o utilizador final é aberta a instalação a partir do Centro de Software.

   ![Notificação personalizada para uma sequência de tarefas](.\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar propriedades de centro de Software
Utilize o procedimento seguinte para configurar os detalhes da sequência de tarefas apresentada no Centro de Software. Estes detalhes são apenas para informação.  
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **geral** separador, as seguintes definições para o Centro de Software estão disponíveis:
  - **Reinício necessário**: Permite ao utilizador saber se é necessário um reinício durante a instalação.
  - **Transferir o tamanho (MB)**: Especifica quantos megabytes é apresentada no Centro de Software para a sequência de tarefas.  
  - **Estimado (minutos) o tempo de execução**: Especifica que o estimado tempo de execução em minutos que é apresentada no Centro de Software para a sequência de tarefas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de ficheiros executáveis a ser executado antes de instalar uma aplicação

No  *<deployment type name>*  **propriedades** caixa de diálogo de um tipo de implementação, no separador Instalar comportamento, pode agora especificar um dos ficheiros executáveis mais que, se a ser executado, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechado automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado.

### <a name="try-it-out"></a>Experimente-o.

1.    Nas propriedades de um tipo de implementação do Configuration Manager, escolha o **instalar comportamento** separador.
2.    Escolher **adicionar** para adicionar um ou mais nomes de ficheiro executável que pretende procurar. Também pode adicionar um nome de apresentação para torná-la mais fácil para os utilizadores a identificar as aplicações na lista.
3.    Se a implementação tiver um objetivo necessário, no Assistente para implementar software, opcionalmente, pode optar por **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação**.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será pedido para fechar qualquer executáveis em execução que especificou antes que podem prosseguir com a instalação.

Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** é selecionada, irá ver uma caixa de diálogo que informa que executáveis especificou são fechados automaticamente quando for atingido o prazo de instalação da aplicação. Pode agendar estas caixas de diálogo no **definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** no **experiência de utilizador** separador da folha de propriedades da implementação.

Se a aplicação foi implementada como **necessário** e a opção **fechar automaticamente qualquer executáveis em execução que especificou no separador de comportamento da instalação da caixa de diálogo Propriedades do tipo de implementação** não estiver selecionada, em seguida, a instalação da aplicação irá falhar se existir uma ou mais das aplicações especificadas estão em execução.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Criar os certificados PFX com suporte de S MIME

Agora pode criar um perfil de certificado PFX que suporte S/MIME e implementá-la aos utilizadores.  Este certificado pode ser utilizado para encriptação S/MIME e a desencriptação em vários dispositivos que o utilizador tem inscritos.

Além disso, pode agora especificar várias autoridades de certificação (AC) em várias funções de sistema de sites de ponto de registo de certificados e, em seguida, atribuir os pedidos de processo CAs como parte do perfil de certificado.

Para dispositivos iOS, pode associar um perfil de certificado PFX para um perfil de e-mail e ativar a encriptação S/MIME.  Em seguida, isto permite S/MIME no cliente de e-mail nativa do iOS e associa o certificado de encriptação S/MIME correto para a mesma.

Para obter mais informações sobre os certificados no Configuration Manager, consulte o artigo [introdução aos perfis de certificado no System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Novas definições de compatibilidade para dispositivos iOS

Foram adicionadas novas definições que pode utilizar nos seus itens de configuração para dispositivos iOS. Estas são as definições que anteriormente existiam no Microsoft Intune numa configuração isolada e estão agora disponíveis ao utilizar o Intune com o Configuration Manager. Se precisar de ajuda com qualquer uma destas definições, consulte o artigo [definições de política de iOS no Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Sincronizar os dados de aplicações geridas para iCloud**
- **Concordam para continuar a atividades no outro dispositivo**
- **iCloud partilha de fotografias**
- **iCloud biblioteca de fotografia**
- **Confiar novo autores de aplicação empresarial**
- **Permitir que o utilizador transfiram conteúdos a partir do arquivo de iBook sinalizado como 'Erotica'** (apenas no modo supervisionado)
- **Forçar emparelhado Apple observa, para utilizar a deteção wrist**
- **Palavra-passe para AirPlay pedidos de envio**
- **Modificar as definições da conta** (apenas no modo supervisionado)
- **Alterações das definições de utilização de dados móveis app** (apenas no modo supervisionado)
- **Apagar todas as definições e conteúdo** (apenas no modo supervisionado)
- **Para configurar as restrições no dispositivo** (apenas no modo supervisionado)
- **Anfitrião de utilização emparelhamento para controlar os dispositivos de um dispositivo iOS pode associá-** (apenas no modo supervisionado)
- **Instalar perfis de configuração e certificados** (apenas no modo supervisionado)
- **Modificação de nome de dispositivo** (apenas no modo supervisionado)
- **Modificação do código de acesso** (apenas no modo supervisionado)
- **O emparelhamento do Apple Watch** (apenas no modo supervisionado)
- **Modificação das definições de notificação** (apenas no modo supervisionado)
- **Imagem de fundo modificação** (apenas no modo supervisionado)
- **Modificação de definições de submissão de diagnóstico** (apenas no modo supervisionado)
- **Modificação Bluetooth** (apenas no modo supervisionado)
- **AirDrop** (apenas no modo supervisionado)
- **Utilizar a Siri ao conteúdo de gerados pelo utilizador de consulta a partir da Internet** (apenas no modo supervisionado)
- **Filtro de blasfémias a Siri** (apenas no modo supervisionado)
- **Devolver resultados a partir da Internet na pesquisa de destaque** (apenas no modo supervisionado)
- **Pesquisa de definição do Word** (apenas no modo supervisionado)
- **Teclados preditiva** (apenas no modo supervisionado)
- **Correção automática** (apenas no modo supervisionado)
- **Verificação ortográfica de teclado** (apenas no modo supervisionado)
- **Atalhos de teclado** (apenas no modo supervisionado)
<!--- - **Enterprise app trust settings modification** --->
- **Instalar aplicações a utilizar o Apple Configurator e iTunes apenas** (apenas no modo supervisionado)
- **Aplicação automática transferências** (apenas no modo supervisionado)
- **Efetuar alterações às definições de aplicação localizar as minhas amigos** (apenas no modo supervisionado)
- **Acesso ao arquivo de iBooks** (apenas no modo supervisionado)
- **Aplicação de mensagens** (apenas no modo supervisionado)
- **Podcasts** (apenas no modo supervisionado)
- **Apple música** (apenas no modo supervisionado)
- **iTunes opção** (apenas no modo supervisionado)
- **Apple notícias** (apenas no modo supervisionado)
- **Centro de jogos** (apenas no modo supervisionado)
- **Tratar AirDrop como um destino de não gerido**

## <a name="android-for-work-support"></a>Android para o suporte de trabalho

A partir da versão de pré-visualização técnica 1702, pode associar uma conta do Google ao seu inquilino do MDM híbrida. Isto permite-lhe fazer o seguinte:

- Inscrever [suportada em dispositivos Android](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android para trabalhar, criação de perfis de trabalho nos dispositivos inscritos
- Aprovar aplicações na Play para o arquivo de trabalho, sincronizá-los com a consola do Configuration Manager e, em seguida, implementá-las aos perfis de trabalho dos dispositivos
- Criar e implementar itens de configuração para configurar definições de perfil e palavra-passe de trabalho para os dispositivos
- Criar e implementar itens de política de conformidade e perfis de acesso a recursos para Android para dispositivos de trabalho como o utilizador já para dispositivos Android
- Executar limpeza seletiva no Android para dispositivos de trabalho

Quando inscreve um dispositivo tal como Android para trabalhar cria um perfil de trabalho no dispositivo que Intune pode gerir. Este perfil de trabalho existe lado a lado com o perfil pessoal no dispositivo Android. Os utilizadores podem facilmente alternar entre aplicações do perfil de trabalho e aplicações de perfis pessoais. Não é possível gerir itens no perfil de pessoal. Aplicações pessoais e os dados permanecem não geridos. O Configuration Manager tem controlo total sobre o perfil de trabalho e o respetivo conteúdo e pode removê-la a partir do dispositivo.

Android para o trabalho é uma plataforma separada a partir do Android e terá de decidir qual a forma de gestão a utilizar para dispositivos Android que suportam perfis de trabalho.

### <a name="try-it-out"></a>Experimente!
As secções seguintes descrevem Android para gestão de trabalho.

#### <a name="enable-android-for-work-management"></a>Ativar Android para gestão de trabalho
1. Crie uma conta do Google https://accounts.google.com/SignUp a utilizar como seu Android para a conta de administrador de trabalho que serão associada a todos os Android trabalho em tarefas de gestão para este inquilino do Intune. Isto pode ser uma conta do Google partilhada entre os administradores que gerem dispositivos Android. Esta é a conta do Google que a organização utiliza para gerir e publicar aplicações no Play para a consola de trabalho. Irá utilizar esta conta para aprovar aplicações na Play para o arquivo de trabalho, por isso, manter um registo de nome de conta e palavra-passe.
2. Ative a inscrição do Android por enlace a conta do Google para o inquilino do Intune gerido no Configuration Manager:
  1. Aceda a **administração** > **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune** e selecione a sua subscrição do Intune.
  2. No Friso, clique em **configurar platformas** > **Android** e certifique-se **inscrição do Android ativar** está selecionada.
  3. No Friso, clique em **configurar platformas** > **Android para trabalhar**.
  4. Na caixa de diálogo, clique em **configurar Android para trabalhar na consola do Intune**. Abre a consola do Intune no seu browser.
  5. Utilize as credenciais de administrador do Intune para iniciar sessão no portal do Intune.
  6. Clique em **configurar** para abrir o Google Play Android para o Web site de trabalho.
  7. No página de sessão da Google, introduza as credenciais da conta Google do passo 1 e, em seguida, forneça as informações da empresa.
3. Quando regressar ao portal do Intune, Android para o trabalho está ativado e tem três opções de inscrição para Android para dispositivos de trabalho:
  - **Gerir todos os dispositivos como Android** - (desativado) Android todos os dispositivos, incluindo dispositivos que suportem Android para trabalhar, irão ser inscritos como dispositivos Android convencionais
  - **Gerir os dispositivos suportados como Android para trabalhar** - (ativado) todos os dispositivos que suportem Android para trabalhar inscritos como Android para dispositivos de trabalho. Todos os dispositivos Android que não suporta Android para o trabalho está inscrito como um dispositivo Android convencional.
  - **Gerir os dispositivos suportados para os utilizadores apenas destes grupos como Android para trabalhar** -(Testing) permite destino Android para gestão de trabalho para um conjunto limitado de utilizadores. Apenas os membros de grupos selecionados que inscreverem um dispositivo que suporte Android para trabalhar são inscritos como Android, para dispositivos de trabalho. Todos os outros são inscritos como dispositivos Android.
  
> [!NOTE]
> Um problema conhecido impede o **gerir dispositivos suportados para os utilizadores apenas destes grupos como Android para trabalhar** opção trabalhem conforme esperado. Os dispositivos dos utilizadores no Azure AD especificado grupos irão inscrever como Android, em vez de Android para trabalhar. Para testar Android para trabalhar, tem de utilizar o **gerir todos os dispositivos suportados como Android para trabalhar**.


  Para poder ativar o Android para a inscrição de trabalho, tem de escolher uma das opções inferior dois. O **gerir dispositivos suportados para os utilizadores apenas destes grupos como Android para trabalhar** opção requer tiver grupos de segurança do Azure Active Directory configure primeiro.

Verá o nome de conta e o nome da organização no portal do Intune quando o enlace está concluído; nesse momento, pode fechar ambos os browsers.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar Android para aplicações de trabalho
Siga estes passos para aprovar aplicações na Play para o arquivo de trabalho, sincronizá-los para a consola do Configuration Manager e implementá-las Android gerido para dispositivos de trabalho. Para implementar aplicações para perfis de utilizador de trabalho, terá de aprovar aplicações da Play para o trabalho e, em seguida, sincronizar as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.
2. Inicie sessão com a conta de administrador do Google vinculada ao seu inquilino do Intune.
3. Procure as aplicações que pretende implementar no seu ambiente e clique em **aprovar** para cada um deles.
4. Na consola do Configuration Manager, aceda a **administrador** > **descrição geral** > **serviços em nuvem** > **Android para trabalhar** e clique em **sincronização**.
5. Aguarde até 10 minutos para as aplicações sincronizar e, em seguida, aceda **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **informações de licença de aplicações da loja**.
6. Clique numa aplicação sincronizada a partir da Play para o trabalho e, em seguida, clique em **Criar aplicação**.
7. Conclua o assistente e clique em **fechar**.
8. Aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**, selecione um Android para aplicações de trabalho e implementar como habitualmente.

Para sincronizar Play para aplicações de trabalho com o Configuration Manager, terá de aprovar, pelo menos, uma aplicação no Play para o Web site de trabalho.

#### <a name="enroll-an-android-for-work-device"></a>Inscrever Android para o dispositivo de trabalho
Como inscrever Android para dispositivos de trabalho é semelhante a inscrição para Android. Transfira e execute a aplicação de Portal da empresa para Android no seu dispositivo móvel. Será pedido para criar um perfil de trabalho como parte do processo de inscrição.  Depois do perfil de trabalho é criado, tem de mudar para a versão do Portal da empresa gerida. O Portal da empresa gerido está etiquetado com um briefcase laranja pequena no canto inferior direito.

#### <a name="create-and-deploy-a-configuration-item"></a>Criar e implementar um item de configuração
Android para trabalhar tem dois grupos de definição para itens de configuração:
- Palavra-passe
- Perfil de trabalho

Pode configurar o conteúdo partilha entre perfis de trabalho, bem como os seguintes itens de configuração em dispositivos com Android 6 ou superior:
- O comportamento para pedir permissões específicas de aplicações
- Se as notificações para aplicações no perfil de trabalho estão visíveis no ecrã de bloqueio

Para efetuar esta operação, crie um item de configuração através do fluxo de trabalho padrão, selecione **Android para trabalhar** no **geral** página e configure as definições para cada um dos grupos de, adicionar o item de configuração para um plano base e implementar como habitualmente. Estas definições serão aplicadas apenas para dispositivos inscritos como Android de trabalho e não as inscritos como Android.

#### <a name="perform-selective-wipe"></a>Executar limpeza seletiva
Os dispositivos inscritos como Android para trabalhar pode apenas ser apagado seletivamente porque só gerir o perfil de trabalho. Isto impede que o perfil pessoal dados serem apagados. Efetuar uma eliminação seletiva num Android para o dispositivo de trabalho remove o perfil de trabalho, incluindo todas as aplicações e dados e unenrolls o dispositivo.

Para apagar seletivamente Android para o dispositivo de trabalho, utilize o normal [processo de eliminação seletiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) na consola do Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemas conhecidos para Android para trabalhar
**Configurar a sincronização agendada no Android as causas de perfis de correio eletrónico de trabalho-los para a implementação falhar** uma das opções na IU do ConfigMgr para Android para perfis de e-mail de trabalho é "Agenda". Noutras plataformas, isto permite que o administrador configurar uma agenda para sincronizar o e-mail e outros dados de conta de correio eletrónico para baixo para os dispositivos móveis que for implementado. No entanto, não funciona para Android para perfis de e-mail do trabalho e escolher qualquer opção diferente de "Não configurada" fará com que o perfil não ser implementada para todos os dispositivos.

