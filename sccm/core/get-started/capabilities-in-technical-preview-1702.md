---
title: Funcionalidades no Technical Preview 1702
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1702.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc1fc6668c61f2eafe04f92fc6b9ea27520ddc43
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1702 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1702. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

Esta pré-visualização introduz novas opções de comentários na consola do Configuration Manager. As opções de comentários permite-lhe enviar comentários diretamente a equipa de desenvolvimento, a título de site de comentários do UserVoice do Configuration Manager.  

>Pode encontrar o **comentários** opção:
-  No Friso, na extremidade esquerda do separador de início de cada nó.  
   ![Friso](./media/feedback-home.png)

-  Quando lhe com o botão direito em qualquer objeto na consola do.   
    ![Opção de clique ecrãs](./media/feedback-option.png)   

Escolher **comentários** abre o seu browser para o site de comentários do UserVoice do Configuration Manager, em https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Alterações para atualizações e manutenção
Os seguintes são introduzidas com esta pré-visualização.

**Opções de atualização mais simples**  
Da próxima vez que qualificam da sua infraestrutura de dois ou mais atualizações, só a atualização mais recente é transferida. Por exemplo, se a versão atual do site é dois ou mais antiga que a versão mais recente está disponível, apenas esse mais recente versão de atualização é transferida automaticamente.  

Tem a opção para transferir e instalar as outras atualizações disponíveis, mesmo quando não estão a versão mais atual. No entanto, irá receber um aviso que a atualização foi substituída por uma mais recente. Para transferir uma atualização que é *disponível para transferência*, selecione a atualização na consola e, em seguida, clique em **transferir**.

**Limpeza melhorada de atualizações anteriores**   
Adicionámos uma função de limpeza automática, que elimina as transferências desnecessárias da pasta 'EasySetupPayload' no seu servidor do site.  


## <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
A partir desta versão, um computador de origem de cache ponto a ponto irão rejeitar um pedido para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer uma das seguintes condições:  
 -  Está no modo de bateria baixo.
 -  Carga da CPU excede 80% momento solicitados.
 -  E/s de disco tem um *AvgDiskQueueLength* excede que 10.
 -  Não existem ligações mais não disponíveis para o computador.   

Pode configurar estas definições utilizando a classe de configuração do agente de cliente para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) ao utilizar o SDK do System Center Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que efetuou irá continuar a pesquisa origens alternativas de formulário de conteúdo no seu conjunto das localizações de origem de conteúdo disponível.   

## <a name="azurediscovery"></a> Utilizar serviços de domínio do Active Directory do Azure para gerir dispositivos, utilizadores e grupos

Com esta pré-visualização técnica versão que pode gerir dispositivos que estão associados a um serviços de domínio do Azure Active Directory (AD) geridos por domínio. Também pode detetar dispositivos, utilizadores e grupos no domínio com vários métodos de deteção do Configuration Manager.

A infraestrutura de pré-visualização técnica de sites, clientes e o domínio de serviços de domínio do Azure AD tem todas executadas no Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Definir a cópia de segurança do Configuration Manager para utilizar o Azure AD
Para utilizar o Azure AD com o Configuration Manager, irá precisar do seguinte:
-   Subscrição do Azure.
-   Azure AD com os serviços de domínio (DS).
-   Um site do Configuration Manager que é executado numa VM do Azure que está associado ao seu Azure AD.
-   Clientes do Configuration Manager que são executados no mesmo ambiente do Azure AD.

Para configurar o serviço de domínio do Azure AD, consulte [começar com os serviços de domínio do Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### <a name="discover-resources"></a>Detetar recursos
Depois de definir a cópia de segurança do Configuration Manager para executar no Azure AD, pode utilizar os seguintes métodos de deteção do Active Directory para procurar o Azure AD para recursos:  
- Deteção de Sistemas do Active Directory
- Deteção de Utilizadores do Active Directory
- Deteção de Grupos do Active Directory  

Para cada método que utilizar, de editar a consulta LDAP para procurar as estruturas do Azure AD UO em vez dos contentores que são normais do Active Directory no local. Isto requer direcionar a consulta para procurar o Active Directory na sua subscrição do Azure.  

Os exemplos seguintes utilizam um Azure AD de *contoso.onmicrosoft.com*:
 - **Deteção de sistemas**   
Azure AD armazena dispositivos sob o **AADDC computadores** UO.  Configure o seguinte:  
  - *LDAP://ou=AADDC computadores, DC = contoso, DC = onmicrosoft, DC = com*  


- **Deteção de utilizadores** AAD armazena utilizadores sob o **AADDC utilizadores** UO.  Configure o seguinte:
  - *LDAP://ou=AADDC utilizadores, DC = contoso, DC = onmicrosoft, DC = com*


- **Deteção de grupos**  
Azure AD não tem uma UO que armazena a grupos. Em vez disso, utilize a mesma estrutura geral como as consultas de sistema ou o utilizador e configurar a consulta LDAP para apontar para a UO que contém os grupos que pretende detetar.

Consulte o seguinte para obter mais informações acerca do Azure AD:  
 - [Serviços de domínio do Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds) em azure.microsoft.com.
 - [Documentação dos serviços de domínio do Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services) em docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Melhoramentos de política de conformidade de dispositivos de acesso condicional

Uma nova regra de política de conformidade de dispositivo está disponível para ajudar a bloquear o acesso aos recursos empresariais que suportam o acesso condicional, quando os utilizadores estão a utilizar aplicações que fazem parte de uma lista de aplicações não conformes. A lista de aplicações não conformes pode ser definida pelo administrador ao adicionar a nova regra de conformidade **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir o **nome da aplicação**, a **ID da aplicação**e o **fabricante da aplicação** (opcional) quando adicionar uma aplicação à lista de não conformidade. Esta definição aplica-se apenas a dispositivos iOS e Android.

Além disso, ajuda as organizações a mitigar a fuga de dados através de aplicações não segura e impedir que o consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivo](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### <a name="try-it-out"></a>Experimente

**Cenário:** Identificar aplicações que poderá estar a causar fugas de dados através do envio de dados da empresa fora da sua empresa ou que estão a causar o consumo excessivo de dados, em seguida, [criar uma política de conformidade de dispositivos de acesso condicional](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) estas aplicações que adiciona a lista de aplicações não conformes. Isto irá bloquear o acesso aos recursos empresariais que suportam o acesso condicional até que o utilizador pode remover a aplicação bloqueada.

## <a name="antimalware-client-version-alert"></a>Alerta de versão de cliente Antimalware
Começando com esta versão de pré-visualização, proteção de ponto final do Gestor de configuração fornece um alerta se tiver mais de 20% (predefinição) dos clientes geridos estiver a utilizar uma versão do cliente antimalware (ou seja, o cliente Windows Defender ou o Endpoint Protection) expirada.

### <a name="try-it-out"></a>Experimente
Certifique-se de que o Endpoint Protection está ativado em todos os clientes de ambiente de trabalho e o servidor através da política de definições de cliente. Agora, pode ver **versão de cliente Antimalware** e **estado de implementação do Endpoint Protection** acedendo **ativos e compatibilidade** > **descrição geral** > **dispositivos** > **todos os ambientes de trabalho e a servir clientes**. Verificar a existência de um alerta, ver **alertas** no **monitorização** área de trabalho. Se mais de 20% dos clientes geridos estão em execução uma versão do antimalware software expirada, a versão de cliente Antimalware está desactualizada é apresentado o alerta. Este alerta não aparecer no **monitorização** > **descrição geral** separador. Para atualizar os clientes de antimalware expirada, ative atualizações de software para clientes de antimalware.

Para configurar a percentagem em que o alerta é gerado, expanda **monitorização** > **alertas** > **todos os alertas**, faça duplo clique em **Antimalware clientes desatualizados** e modificar o **emitir um alerta se a percentagem de clientes geridos com uma versão desatualizada do cliente antimalware é mais do que** opção.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Avaliação de compatibilidade para o Windows Update para atualizações de negócio
Agora, pode configurar uma regra de atualização de política de conformidade para incluir uma atualização do Windows para o resultado da avaliação de negócio como parte da avaliação de acesso condicional.
> [!IMPORTANT]
> Tem de ter o Windows 10 internas de pré-visualização 15019 ou posterior para utilizar a avaliação de compatibilidade para o Windows Update para atualizações de negócio.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir atualização do Windows para empresas gerir atualizações do Windows 10
Para recolher informações de avaliação de compatibilidade para o Windows Update para atualizações de negócio, utilize o procedimento seguinte para configurar o definição para permitir explicitamente o Windows Update para empresas gerir atualizações do Windows 10 do agente de cliente.
1. Na consola do Configuration Manager, aceda a **Administração** > **Definições do Cliente**.
2. Nas propriedades para as definições de cliente, aceda a **atualizações de Software**e selecione **Sim** para o **de atualizações de gerir o Windows 10 com o Windows Update para empresas** definição.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Criar uma política de conformidade para o Windows Update para avaliação de negócio
1. Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **as definições de compatibilidade** > **políticas de conformidade**.
2. Clique em **criar política de conformidade** ou selecione uma política de conformidade existente para modificar.
3. Na página geral, forneça um nome e uma descrição, selecione **regras de compatibilidade para dispositivos geridos com o cliente do Configuration Manager**, definir a gravidade de incompatibilidade para relatórios e, em **seguinte**.
4. Na página de plataformas suportadas, selecione **Windows 10**e, em seguida, clique em **seguinte**.
5. Na página de regras, clique em **novo...** e, em seguida, para **condição** escolha **requerem o Windows Update para compatibilidade de negócio**. O **valor** definição é automaticamente definida para **verdadeiro**.

A nova política é apresentada no nó **Políticas de Conformidade** da área de trabalho **Ativos e Compatibilidade** .

### <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade
1. Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **as definições de compatibilidade**e, em seguida, clique em **políticas de conformidade**.
2. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.
3. Na caixa de diálogo **Implemente a Política de Conformidade** , clique em **Procurar** para selecionar a coleção de utilizadores na qual a política será implementada.
   Além disso, pode selecionar opções de geração de alertas quando a política não está em conformidade, bem como configurar a agenda com base na qual a política será avaliada em termos de conformidade.
4. Quando tiver terminado, clique em **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade
Depois de criar a política de conformidade, pode monitorizar os resultados de compatibilidade na consola do Configuration Manager. Para obter mais informações, consulte [monitorizar a política de conformidade](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Melhoramentos às definições do Centro de Software e mensagens de notificação para sequências de tarefas de elevado impacto
Esta versão inclui os seguintes melhoramentos para mensagens de notificação para sequências de tarefas de implementação de elevado impacto e de definições do Centro de Software:

- Nas propriedades para a sequência de tarefas, agora pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas de sistema não operacionais, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpra determinadas condições é automaticamente definida como impacto elevado. Para obter mais informações, consulte [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades para a sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou criar a sua própria mensagem de notificação personalizada para implementações de elevado impacto.
- Nas propriedades para a sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem efetuar um reinício necessário, o tamanho de transferência da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de elevado impacto predefinida para direta atualiza agora os Estados que as aplicações, dados e definições são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo for indicado que todas as aplicações, dados e as definições serão perdidas, que não era aplica-se uma atualização no local.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de elevado impacto
Utilize o procedimento seguinte para definir uma sequência de tarefas como de elevado impacto.
> [!NOTE]
> Qualquer sequência de tarefas que cumpra determinadas condições é automaticamente definida como impacto elevado. Para obter mais informações, consulte [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, vá para **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **esta é uma sequência de tarefas de elevado impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação para implementações de alto risco
1. Na consola do Configuration Manager, vá para **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **notificação do utilizador** separador, selecione **utilizar texto personalizado**.
>  [!NOTE]
>  Só é possível definir texto de notificação do utilizador quando o **esta é uma sequência de tarefas de elevado impacto** está selecionada.

4. Configure as seguintes definições (máximo de 255 carateres para cada caixa de texto):

   **Texto do título de notificação de utilizador**: Especifica o texto azul que apresenta na notificação de utilizador do Centro de Software. Por exemplo, a predefinição de notificação de utilizador, esta secção contém algo semelhante a "Confirmar que pretende atualizar o sistema operativo neste computador".

   **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornecem o corpo da notificação personalizada.
   - caixa de texto 1ª: Especifica o corpo do principal de texto, normalmente, que contém instruções para o utilizador. Por exemplo, a predefinição de notificação de utilizador, esta secção contém algo como "a atualização do sistema operativo irá demorar tempo e o computador poderá reiniciar várias vezes."
   - caixa de texto 2nd: Especifica o texto a negrito no corpo do principal do texto. Por exemplo, a predefinição de notificação de utilizador, esta secção contém algo como "esta atualização no local instala o novo sistema operativo e migra automaticamente as suas definições, aplicações e dados."
   - caixa de texto 3rd: Especifica a última linha de texto com o texto a negrito. Por exemplo, a predefinição de notificação de utilizador, esta secção contém algo semelhante a "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   

   Vamos supor que configura a seguinte notificação personalizada nas propriedades.

   ![Notificação personalizada para uma sequência de tarefas](.\media\user-notification.png)

   Será apresentada a seguinte mensagem de notificação quando o utilizador final abre a instalação do Centro de Software.

   ![Notificação personalizada para uma sequência de tarefas](.\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar propriedades de centro de Software
Utilize o procedimento seguinte para configurar os detalhes para a sequência de tarefas apresentadas no Centro de Software. Estes detalhes estão apenas para informação.  
1. Na consola do Configuration Manager, vá para **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. No **geral** separador, estão disponíveis as seguintes definições no Centro de Software:
  - **Reinício necessário**: Permite que o utilizador saber se é necessário reiniciar durante a instalação.
  - **Transferir o tamanho (MB)**: Especifica a quantidade de megabytes é apresentada no Centro de Software para a sequência de tarefas.  
  - **Estimado (minutos) o tempo de execução**: Especifica que o estimado tempo de execução em minutos, que é apresentado no Centro de Software para a sequência de tarefas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação

No *<deployment type name>* **propriedades** caixa de diálogo de um tipo de implementação, no separador Instalar comportamento, agora pode especificar um dos ficheiros executáveis mais que, se em execução, irão bloquear a instalação do tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechada automaticamente para implementações com um objetivo necessário) antes da implementação tipo pode ser instalado.

### <a name="try-it-out"></a>Experimente.

1.  Nas propriedades de um tipo de implementação do Configuration Manager, escolha o **instalar comportamento** separador.
2.  Escolha **adicionar** para adicionar um ou mais nomes de ficheiro executável que pretende procurar. Também pode adicionar um nome a apresentar para o tornar mais fácil para os utilizadores identificar aplicações na lista.
3.  Se a implementação tiver um objetivo necessário, o Assistente de implementação de software, opcionalmente, pode optar por **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação**.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será pedido para fechar a qualquer executáveis em execução, especificado antes de poderão avançar com a instalação.

Se a aplicação foi implementada como **necessário**e a opção **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação** é selecionado, verá uma caixa de diálogo que os informa de que executáveis que especificou são fechados automaticamente quando é atingido o prazo de instalação da aplicação. Pode agendar estas caixas de diálogo no **as definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** no **experiência de utilizador** separador de propriedades da implementação.

Se a aplicação foi implementada como **necessário** e a opção **fechar automaticamente quaisquer executáveis em execução, especificado no separador de comportamento de instalação de caixa de diálogo de propriedades do tipo de implementação** não estiver selecionada, em seguida, a instalação da aplicação irá falhar se um ou mais das aplicações especificadas estão em execução.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Criar os certificados PFX com suporte de S MIME

Agora pode criar um perfil de certificado PFX suporta S/MIME e implementá-la aos utilizadores.  Este certificado, em seguida, pode ser utilizado para encriptação S/MIME e desencriptação em todos os dispositivos que o utilizador tenha inscrito.

Além disso, pode agora especificar várias autoridades de certificação (AC) em várias funções de sistema de sites de ponto de registo de certificados e, em seguida, atribuir os pedidos de processo do ACS como parte do perfil de certificado.

Para dispositivos iOS, pode associar um perfil de certificado PFX para um perfil de e-mail e ativar a encriptação S/MIME.  Em seguida, isto permite que o S/MIME do cliente de e-mail nativa no iOS e associa o certificado de encriptação S/MIME correto para a mesma.

Para obter mais informações sobre os certificados no Configuration Manager, consulte [introdução aos perfis de certificado no System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Novas definições de conformidade para dispositivos iOS

Adicionámos novas definições, que pode utilizar os itens de configuração para dispositivos iOS. Estas são as definições que existiam no Microsoft Intune numa configuração autónoma e anteriormente estão agora disponíveis ao utilizar o Intune com o Configuration Manager. Se precisar de ajuda com qualquer uma destas definições, consulte [definições de política do iOS no Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Sincronizar os dados de aplicações geridas para iCloud**
- **Handoff continue as atividades outro dispositivo**
- **Partilha de fotografias do iCloud**
- **Biblioteca de fotografias do iCloud**
- **Os autores de aplicação do novo enterprise de confiança**
- **Permitir que o utilizador transfira conteúdos da loja iBook sinalizado como "Erótico"** (modo supervisionado apenas)
- **Forçar emparelhado observa Apple para utilizar a deteção de wrist**
- **Palavra-passe para AirPlay pedidos de envio**
- **Modificar as definições da conta** (modo supervisionado apenas)
- **Alterações das definições de utilização de dados via rede móvel aplicação** (modo supervisionado apenas)
- **Apagar todos os conteúdos e definições** (modo supervisionado apenas)
- **Configure as restrições no dispositivo** (modo supervisionado apenas)
- **Utilize emparelhamento de anfitrião para controlar os dispositivos um dispositivo iOS pode ser emparelhado com** (modo supervisionado apenas)
- **Instalar a configuração de perfis e certificados** (modo supervisionado apenas)
- **Modificação de nome de dispositivo** (modo supervisionado apenas)
- **Modificação do código de acesso** (modo supervisionado apenas)
- **O emparelhamento do Apple Watch** (modo supervisionado apenas)
- **Modificação das definições de notificação** (modo supervisionado apenas)
- **Imagem de fundo modificação** (modo supervisionado apenas)
- **Modificação de definições de submissão de diagnóstico** (modo supervisionado apenas)
- **Modificação de Bluetooth** (modo supervisionado apenas)
- **AirDrop** (modo supervisionado apenas)
- **Utilize a siri Consulte conteúdos gerados pelo utilizador de consulta da Internet** (modo supervisionado apenas)
- **Filtro de profanity Siri** (modo supervisionado apenas)
- **Devolver resultados da Internet na pesquisa Spotlight** (modo supervisionado apenas)
- **Pesquisa de definição de palavra** (modo supervisionado apenas)
- **Teclados preditivos** (modo supervisionado apenas)
- **Correção automática** (modo supervisionado apenas)
- **Teclado verificação ortográfica** (modo supervisionado apenas)
- **Atalhos de teclado** (modo supervisionado apenas)
<!--- - **Enterprise app trust settings modification** --->
- **Instalar aplicações com o Apple Configurator e apenas iTunes** (modo supervisionado apenas)
- **Aplicação automática transferências** (modo supervisionado apenas)
- **Efetuar alterações às definições da aplicação encontrar amigos** (modo supervisionado apenas)
- **Acesso à loja iBooks** (modo supervisionado apenas)
- **Aplicação mensagens** (modo supervisionado apenas)
- **Podcasts** (modo supervisionado apenas)
- **Música Apple** (modo supervisionado apenas)
- **botões de opção do iTunes** (modo supervisionado apenas)
- **Apple notícias** (modo supervisionado apenas)
- **Centro de jogos** (modo supervisionado apenas)
- **Tratar AirDrop como um destino de não gerido**

## <a name="android-for-work-support"></a>Android para o suporte de trabalho

A partir da versão de pré-visualização técnica 1702, é possível vincular uma conta do Google no seu inquilino MDM híbrida. Isto permite-lhe fazer o seguinte:

- Inscrever [dispositivos Android suportados](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android de trabalho, a criação de perfis de trabalho nos dispositivos inscritos
- Aprovar aplicações na Play para o arquivo de trabalho, sincronizá-las com a consola do Configuration Manager e, em seguida, implementá-las para perfis de trabalho dos dispositivos
- Criar e implementar itens de configuração para configurar definições de perfil e a palavra-passe de trabalho para esses dispositivos
- Criar e implementar itens de política de conformidade e perfis de acesso a recursos para Android para dispositivos de trabalho, já fazê-lo para dispositivos Android
- Executar a eliminação seletiva no Android para dispositivos de trabalho

Quando inscreve um dispositivo como Android para trabalho cria um perfil de trabalho no dispositivo que o Intune pode gerir. Este perfil de trabalho existe lado lado a lado com o perfil pessoal no dispositivo Android. Os utilizadores podem facilmente mudar entre aplicações do perfil de trabalho e aplicações pessoais perfil. Não é possível gerir itens no perfil de pessoal. Aplicações pessoais e os dados permanecem não geridos. O Configuration Manager tem controlo total sobre o perfil de trabalho e o respetivo conteúdo e removê-lo do dispositivo.

Android para o trabalho é uma plataforma separada do Android, e terá de decidir a forma da gestão a utilizar para dispositivos Android que suportam perfis de trabalho.

### <a name="try-it-out"></a>Experimente!
As secções seguintes descrevem Android para gestão de trabalho.

#### <a name="enable-android-for-work-management"></a>Ativar Android para gestão de trabalho
1. Criar uma conta do Google na https://accounts.google.com/SignUp para utilizar como Android para a conta de administrador de trabalho que será associada ao Android todas as tarefas de gestão de trabalho para este inquilino Intune. Isto pode ser uma conta do Google partilhada entre os administradores que gerem os dispositivos Android. Esta é a conta do Google pela sua organização para gerir e publicar aplicações na Play para a consola de trabalho. Irá utilizar esta conta para aprovar aplicações na Play para o arquivo de trabalho, por isso, manter controlar do nome da conta e palavra-passe.
2. Ative a inscrição de dispositivos Android através do enlace a conta do Google para o inquilino do Intune gerido no Configuration Manager:
  1. Aceda a **administração** > **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune** e selecione a sua subscrição do Intune.
  2. No Friso, clique em **configurar plataformas** > **Android** e certifique-se **ativar inscrição Android** está marcada.
  3. No Friso, clique em **configurar plataformas** > **Android para trabalho**.
  4. Na caixa de diálogo, clique em **configurar Android para o trabalho na consola do Intune**. Abre a consola do Intune no seu browser.
  5. Utilize as suas credenciais de administrador do Intune para iniciar sessão no portal do Intune.
  6. Clique em **configurar** para abrir o Android da Google Play para o Web site de trabalho.
  7. Da Google-na página sessão, introduza as credenciais da conta Google do passo 1 e, em seguida, forneça as informações da sua empresa.
3. Quando regressar ao portal do Intune, o Android para o trabalho está ativado e tem três opções de inscrição para Android para dispositivos de trabalho:
  - **Gerir todos os dispositivos como Android** - (desativado) Android todos os dispositivos, incluindo dispositivos que suportam o Android for Work, que irão ser inscritos como dispositivos Android convencionais
  - **Gerir os dispositivos suportados como Android para trabalho** - (ativado) todos os dispositivos que suportam o Android de trabalho são inscritos como Android, para dispositivos de trabalho. Todos os dispositivos Android que não suporta Android para o trabalho está inscrito como um dispositivo Android convencional.
  - **Gerir os dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** -permite (teste) de destino Android para gestão de trabalho para um conjunto limitado de utilizadores. Apenas os membros de grupos selecionados que inscreverem um dispositivo que suporta o Android de trabalho são inscritos como Android, para dispositivos de trabalho. Todos os outros são inscritos como dispositivos Android.
  
> [!NOTE]
> Um problema conhecido impede o **gerir dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** opção de funcionar conforme esperado. Os dispositivos dos utilizadores no Azure AD especificado grupos irão inscrever como Android, em vez de Android para o trabalho. Para testar o Android de trabalho, tem de utilizar o **gerir todos os dispositivos suportados como Android para trabalho**.


  Para ativar o Android para a inscrição de trabalho, tem de escolher uma das opções na parte inferior dois. O **gerir dispositivos suportados para apenas os utilizadores nestes grupos como Android para trabalho** opção requer que tem de configurar primeiro os grupos de segurança do Azure Active Directory.

Verá o nome de conta e o nome da organização no portal do Intune depois de concluída; o enlace nessa altura, pode fechar ambos os browsers.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar Android para aplicações de trabalho
Siga estes passos para aprovar aplicações na Play para o arquivo de trabalho, sincronizá-los para a consola do Configuration Manager e implementá-las para o Android gerida para dispositivos de trabalho. Para implementar aplicações para perfis de utilizador de trabalho, terá de aprovar as aplicações na Play para o trabalho e, em seguida, sincronizar as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.
2. Inicie sessão com a conta de administrador do Google vinculado ao seu inquilino do Intune.
3. Procure as aplicações que pretende implementar no seu ambiente e clique em **aprovar** para cada um deles.
4. Na consola do Configuration Manager, vá para **administrador** > **descrição geral** > **serviços em nuvem** > **Android para trabalho** e clique em **sincronização**.
5. Aguarde até 10 minutos para as aplicações sincronizar e, em seguida, avance **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **informações de licença para aplicações da loja**.
6. Clique numa aplicação sincronizada a partir da Play para o trabalho e, em seguida, clique em **Criar aplicação**.
7. Conclua o assistente e clique em **fechar**.
8. Aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**, selecione um Android para aplicações de trabalho e implementar como habitualmente.

Para sincronizar Play para aplicações de trabalho com o Configuration Manager, necessitará de aprovar pelo menos uma aplicação na Play para o Web site de trabalho.

#### <a name="enroll-an-android-for-work-device"></a>Inscrever um Android para dispositivos de trabalho
Como inscrever o Android para dispositivos de trabalho é semelhante a inscrição para Android. Transfira e execute a aplicação Portal da empresa para Android no seu dispositivo móvel. Será solicitado para criar um perfil de trabalho como parte do processo de inscrição.  Assim que o perfil de trabalho é criado, tem de mudar para a versão do Portal da empresa gerida. O Portal da empresa geridos é marcado com um pequeno briefcase laranja no canto inferior direito.

#### <a name="create-and-deploy-a-configuration-item"></a>Criar e implementar um item de configuração
Android de trabalho tem dois grupos de definições para itens de configuração:
- Palavra-passe
- Perfil de trabalho

Pode configurar o conteúdo de partilha entre perfis de trabalho, bem como os seguintes itens de configuração em dispositivos com Android 6 ou superior:
- O comportamento para solicitar permissões específicas de aplicações
- Indica se as notificações para aplicações no perfil de trabalho são visíveis no ecrã de bloqueio

Para experimentar isto, crie um item de configuração através do fluxo de trabalho padrão, escolha **Android para trabalho** no **geral** página e configurar as definições para cada um dos grupos de definições, adicionar o item de configuração para uma linha de base e implementar como habitualmente. Estas definições apenas se aplica a dispositivos inscritos como Android, para e de trabalho não os que são inscritos como Android.

#### <a name="perform-selective-wipe"></a>Executar a eliminação seletiva
Os dispositivos inscritos como Android para trabalho só poderem ser apagados seletivamente porque apenas a gerir o perfil de trabalho. Esta ação protege o perfil pessoal dados serem apagados. A eliminação seletiva num Android para dispositivos de trabalho remove o perfil de trabalho, incluindo todas as aplicações e dados e é removido do dispositivo.

Para apagar seletivamente um Android para dispositivos de trabalho, utilize o normal [processo de eliminação seletiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) na consola do Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemas conhecidos para Android para o trabalho
**Configurar a sincronização agendada no Android para causas de perfis de e-mail de trabalho para efetuar para implementar** é uma das opções na IU do ConfigMgr para Android para perfis de e-mail de trabalho "Agenda". Noutras plataformas, isto permite que o administrador configurar uma agenda para a sincronizar o e-mail e outros dados de conta de e-mail para dispositivos móveis que é implementado. No entanto, não funciona para Android para perfis de e-mail de trabalho e selecionar qualquer opção que não seja "Não configurada" fará com que o perfil a não ser implementada para todos os dispositivos.
