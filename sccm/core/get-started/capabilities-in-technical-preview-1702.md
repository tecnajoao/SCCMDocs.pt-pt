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
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d817bf27302b0a894eb834c747fb3bbcb0ad3fa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141192"
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1702 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1702. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Enviar comentários a partir da consola do Configuration Manager

Esta pré-visualização apresenta novas opções de comentários na consola do Configuration Manager. As opções de comentários permite que envie comentários diretamente para a equipe de desenvolvimento, por meio do site de comentários do UserVoice do Configuration Manager.  

> Pode encontrar os **comentários** opção:
> -  No Friso, na extremidade esquerda do separador base de cada nó.  
>    ![Faixa de opções](./media/feedback-home.png)

-  Quando com o botão direito em qualquer objeto na consola do.   
    ![Opção de clique Righ](./media/feedback-option.png)   

Escolher **comentários** abre-se o browser para o site de comentários do UserVoice do Configuration Manager, em https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Alterações para atualizações e manutenção
A seguir é introduzida com esta pré-visualização.

**Opções de atualização mais simples**  
Da próxima vez que sua infraestrutura é elegível para dois ou mais atualizações, apenas a atualização mais recente é transferida. Por exemplo, se a sua versão atual do site é dois ou mais anterior à versão mais recente disponível, apenas nessa versão de atualização mais recente é transferida automaticamente.  

Tem a opção para transferir e instalar as outras atualizações disponíveis, mesmo quando não estão a versão mais atual. No entanto, receberá um aviso de que a atualização foi substituída por uma mais recente. Para transferir uma atualização que está *disponível para Download*, selecione a atualização na consola e, em seguida, clique em **transferir**.

**Melhorada a limpeza das atualizações mais antigas**   
Adicionámos uma função de limpeza automática, que elimina transferências desnecessárias da pasta "EasySetupPayload" no servidor de site.  


## <a name="peer-cache-improvements"></a>Melhorias da Cache ponto a ponto
Começando com esta versão, um computador de origem de cache ponto a ponto irão rejeitar um pedido para o conteúdo quando o computador de origem de cache ponto a ponto cumpre qualquer um dos seguintes condições:  
 -  Está no modo de pouca bateria.
 -  Carga da CPU excede 80%, no momento que o conteúdo é solicitado.
 -  E/s de disco tem um *AvgDiskQueueLength* que excede a 10.
 -  Não existem ligações não é mais disponíveis para o computador.   

Pode configurar essas configurações usando a classe de configuração do agente de cliente para a funcionalidade de origem do elemento de rede (*SMS_WinPEPeerCacheConfig*) ao utilizar o SDK do System Center Configuration Manager.

Quando o computador rejeita um pedido para o conteúdo, o computador que irá continuar a procurar origens alternativas de formulário de conteúdo em seu pool de localizações de origem de conteúdo disponível.   

## <a name="azurediscovery"></a> Utilizar o Azure Active Directory Domain Services para gerir dispositivos, utilizadores e grupos

Com esta pré-visualização técnica versão que pode gerir dispositivos que estão associados a um serviços de domínio do Azure Active Directory (AD) o domínio gerido. Também pode detetar dispositivos, utilizadores e grupos no domínio com vários métodos de deteção do Configuration Manager.

A infraestrutura do site de pré-visualização técnica, os clientes e o domínio do Azure AD Domain Services têm todos executados no Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Definir o Gestor de configuração para utilizar o Azure AD
Para utilizar o Azure AD com o Configuration Manager, precisará do seguinte:
-   Subscrição do Azure.
-   O Azure AD Domain Services (DS).
-   Um site do Configuration Manager que é executada numa VM do Azure que está associado ao seu Azure AD.
-   Clientes do Configuration Manager que são executados no mesmo ambiente do Azure AD.

Para configurar o serviço de domínio do Azure AD, consulte [introdução ao Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### <a name="discover-resources"></a>Detetar recursos
Depois de definir o Gestor de configuração para ser executado no Azure AD, pode utilizar os seguintes métodos de deteção do Active Directory para o Azure AD para recursos de pesquisa:  
- Deteção de Sistemas do Active Directory
- Deteção de Utilizadores do Active Directory
- Deteção de Grupos do Active Directory  

Para cada método utilizado, edite a consulta LDAP para procurar as estruturas de UO do Azure AD em vez dos contentores que são característicos para Active Directory no local. Isto requer a direcionar a consulta para procurar o Active Directory na sua subscrição do Azure.  

Os exemplos seguintes utilizam um Azure AD de *contoso.onmicrosoft.com*:
- **Deteção de sistemas**   
  Azure AD armazena dispositivos sob o **computadores do aad DC** UO.  Configure o seguinte:  
  - *LDAP://ou=AADDC computadores, DC = contoso, DC = onmicrosoft, DC = com*  


- **Deteção de utilizadores** AAD armazena usuários sob os **utilizadores do aad DC** UO.  Configure o seguinte:
  - *Os utilizadores de LDAP://ou=AADDC, DC = contoso, DC = onmicrosoft, DC = com*


- **Deteção de grupos**  
O Azure AD não tem uma UO que armazena a grupos. Em vez disso, utilize a mesma estrutura geral das consultas de sistema ou o utilizador e configurar a consulta LDAP para apontar para a UO que contenha os grupos que pretende detetar.

Veja o seguinte para obter mais informações sobre o Azure AD:  
 - [Serviços de domínio do Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds) em azure.microsoft.com.
 - [Documentação dos serviços de domínio do Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services) no docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Melhorias de política de conformidade de dispositivo de acesso condicional

Uma nova regra de política de conformidade do dispositivo está disponível para o ajudar a bloquear o acesso a recursos da empresa que suportam o acesso condicional, quando os utilizadores estão a utilizar aplicações que fazem parte de uma lista de em não conformidades de aplicações. A lista de em não conformidades de aplicações pode ser definida pelo administrador, ao adicionar a nova regra de conformidade **aplicações que não não possível instalar**. Esta regra requer que o administrador para introduzir os **nome da aplicação**, o **ID de aplicação**e o **publicador da aplicação** (opcional) ao adicionar uma aplicação à lista de não conformidade. Esta definição aplica-se apenas a dispositivos iOS e Android.

Além disso, esta definição ajuda as organizações a reduzir a fuga de dados através de aplicações não protegidas e a impedir o consumo excessivo de dados através de determinadas aplicações.

- Saiba mais [como funcionam as políticas de conformidade do dispositivo](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Saiba mais [como criar políticas de conformidade de dispositivos](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### <a name="try-it-out"></a>Experimentar

**Cenário:** Identificar aplicações que poderá estar a causar vazamento de dados através do envio de dados da empresa fora da sua empresa ou que estão a causar o consumo excessivo de dados, em seguida, [criar uma política de conformidade de dispositivos de acesso condicional](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) que adiciona estas aplicações para o lista de em não conformidades de aplicações. Esta ação vai bloquear o acesso aos recursos empresariais que suportam o acesso condicional até que o utilizador pode remover a aplicação bloqueada.

## <a name="antimalware-client-version-alert"></a>Alerta de versão do cliente de antimalware
A partir desta versão de pré-visualização, proteção de ponto final do Gestor de configuração fornece um alerta se tiver mais de 20% (predefinição) de clientes geridos estão a utilizar uma versão expirada do cliente de antimalware (ou seja, o cliente do Windows Defender ou o Endpoint Protection).

### <a name="try-it-out"></a>Experimentar
Certifique-se de que o Endpoint Protection está ativada em todos os clientes de Desktops e servidores, utilizando a política de definições de cliente. Agora, pode ver **versão de cliente de Antimalware** e **estado de implementação do Endpoint Protection** indo **ativos e compatibilidade**  >   **Descrição geral** > **dispositivos** > **todos os computadores de secretária e servir clientes**. Para verificar a existência de um alerta, ver **alertas** no **monitorização** área de trabalho. Se mais de 20% de clientes geridos com uma versão de expirada do antimalware software, a versão de cliente de Antimalware está desatualizada é apresentado o alerta. Este alerta não aparece no **monitorização** > **descrição geral** separador. Para atualizar os clientes de antimalware expirada, ative atualizações de software para clientes de antimalware.

Para configurar a percentagem em que o alerta é gerado, expanda **monitorização** > **alertas** > **todos os alertas**, faça duplo clique em  **Os clientes de antimalware desatualizados** e modificar o **emitir um alerta se a percentagem de clientes geridos com uma versão desatualizada do cliente de antimalware for superior** opção.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Avaliação de compatibilidade para o Windows Update para atualizações de negócios
Agora pode configurar uma regra de atualização de política de conformidade para incluir uma atualização do Windows para o resultado da avaliação de negócio como parte da avaliação de acesso condicional.
> [!IMPORTANT]
> Tem de ter o Windows 10 Insider Preview Build 15019 ou posterior para utilizar a avaliação de conformidade para o Windows Update para atualizações de negócios.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Permitir que o Windows Update para empresas para gerir atualizações do Windows 10
Para recolher informações de avaliação de conformidade para o Windows Update para atualizações de negócios, utilize o procedimento seguinte para configurar o agente de cliente na definição de permitir explicitamente o Windows Update para empresas para gerir atualizações do Windows 10.
1. Na consola do Configuration Manager, aceda a **Administração** > **Definições do Cliente**.
2. Nas propriedades para as definições de cliente, aceda a **atualizações de Software**e selecione **Sim** para o **atualizações de gerir o Windows 10 com o Windows Update para empresas** definição.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Criar uma política de conformidade para o Windows Update para avaliação de negócios
1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **definições de compatibilidade** > **políticas de conformidade**.
2. Clique em **criar política de conformidade** ou selecione uma política de conformidade existente para modificar.
3. Na página geral, forneça um nome e uma descrição, selecione **regras de conformidade para dispositivos geridos com o cliente de Configuration Manager**, definir a gravidade de incompatibilidade para relatórios e clique em **próxima** .
4. Na página de plataformas suportadas, selecione **Windows 10**e, em seguida, clique em **próxima**.
5. Na página de regras, clique em **New...** e, em seguida, para **condição** escolha **exigem Windows conformidade Update para empresas**. O **valor** definição é automaticamente definida como **verdadeiro**.

A nova política é apresentada no nó **Políticas de Conformidade** da área de trabalho **Ativos e Compatibilidade** .

### <a name="deploy-a-compliance-policy"></a>Implementar uma política de conformidade
1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **definições de compatibilidade**e, em seguida, clique em **políticas de conformidade**.
2. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.
3. Na caixa de diálogo **Implemente a Política de Conformidade** , clique em **Procurar** para selecionar a coleção de utilizadores na qual a política será implementada.
   Além disso, pode selecionar opções de geração de alertas quando a política não está em conformidade, bem como configurar a agenda com base na qual a política será avaliada em termos de conformidade.
4. Quando tiver terminado, clique em **OK**.

### <a name="monitor-the-compliance-policy"></a>Monitorizar a política de conformidade
Depois de criar a política de conformidade, pode monitorizar os resultados de compatibilidade na consola do Configuration Manager. Para obter detalhes, consulte [monitorizar a política de conformidade](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Melhorias para as definições do Centro de Software e mensagens de notificação para sequências de tarefas de alto impacto
Esta versão inclui as seguintes melhorias às definições do Centro de Software e mensagens de notificação para sequências de tarefas de implementação de alto impacto:

- Nas propriedades da sequência de tarefas, agora, pode configurar qualquer sequência de tarefas, incluindo sequências de tarefas de sistema não operacionais, como uma implementação de alto risco. Qualquer sequência de tarefas que cumpre determinadas condições automaticamente é definida como alto impacto. Para obter detalhes, consulte [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Nas propriedades da sequência de tarefas, pode optar por utilizar a mensagem de notificação predefinidas ou criar sua própria mensagem de notificação personalizada para implementações de alto impacto.
- Nas propriedades da sequência de tarefas, pode configurar o Centro de Software propriedades, que incluem fazer um reinício necessário, o tamanho de download da sequência de tarefas, e o estimado tempo de execução.
- A mensagem de implementação de alto impacto predefinida para in-loco atualiza agora os Estados que aplicações, dados e definições são migradas automaticamente. Anteriormente, a mensagem predefinida para qualquer instalação do sistema operativo indicado que todas as aplicações, dados e definições seriam perdidas, que não era válido para uma atualização no local.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Definir uma sequência de tarefas como uma sequência de tarefas de alto impacto
Utilize o procedimento seguinte para definir uma sequência de tarefas como alto impacto.
> [!NOTE]
> Qualquer sequência de tarefas que cumpre determinadas condições automaticamente é definida como alto impacto. Para obter detalhes, consulte [gerir implementações de alto risco](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **notificação do utilizador** separador, selecione **trata de uma sequência de tarefas de alto impacto**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Criar uma notificação para implementações de alto risco
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **notificação do utilizador** separador, selecione **utilizar texto personalizado**.
   > [!NOTE]
   >  Apenas pode definir o texto de notificação do utilizador quando o **esta é uma sequência de tarefas de alto impacto** está selecionada.

4. Configure as seguintes definições (máx. de 255 carateres para cada caixa de texto):

   **Texto do cabeçalho de notificação de utilizador**: Especifica o texto azul que apresenta a notificação de utilizador do Centro de Software. Por exemplo, a notificação de utilizador padrão, esta secção contém algo como "Confirmar que pretende atualizar o sistema operativo neste computador".

   **Texto de mensagem de notificação do utilizador**: Existem três caixas de texto que fornecem o corpo da notificação personalizado.
   - 1º de caixa de texto: Especifica o corpo principal do texto, normalmente, que contém instruções para o utilizador. Por exemplo, a notificação de utilizador padrão, esta secção contém algo como "atualização do sistema operativo irá demorar algum tempo e o computador poderá reiniciar várias vezes."
   - caixa de texto 2nd: Especifica o texto em negrito no corpo principal do texto. Por exemplo, a notificação de utilizador padrão, esta secção contém algo como "esta atualização no local instala o novo sistema operativo e migra automaticamente as suas aplicações, dados e definições."
   - caixa de texto 3º: Especifica a última linha de texto sob o texto em negrito. Por exemplo, na notificação de utilizador padrão, esta secção contém algo como "clique em instalar para iniciar. Caso contrário, clique em Cancelar."   

   Digamos que configura a seguinte notificação personalizada nas propriedades.

   ![Notificação personalizada para uma sequência de tarefas](./media/user-notification.png)

   A seguinte mensagem de notificação será apresentada quando o utilizador final abre a instalação do Centro de Software.

   ![Notificação personalizada para uma sequência de tarefas](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurar as propriedades do Centro de Software
Utilize o procedimento seguinte para configurar os detalhes para a sequência de tarefas apresentadas no Centro de Software. Esses detalhes são apenas para informação.  
1. Na consola do Configuration Manager, aceda a **biblioteca de Software** > **sistemas operativos** > **sequências de tarefas**.
2. Selecione a sequência de tarefas para editar e clique em **propriedades**.
3. Sobre o **gerais** guia, as seguintes definições para o Centro de Software estão disponíveis:
   - **Reinício necessário**: Permite ao utilizador saber se é necessário reiniciar durante a instalação.
   - **Tamanho (MB) de download**: Especifica o número de megabytes é apresentada no Centro de Software para a sequência de tarefas.  
   - **Estimado (minutos) de tempo de execução**: Especifica que o estimado tempo de execução em minutos, que é apresentado no Centro de Software para a sequência de tarefas.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação

Na *<deployment type name>* **propriedades** caixa de diálogo de um tipo de implementação, no separador de comportamento de instalação, pode agora especificar uma das mais ficheiros executáveis que, se executar, irão bloquear a instalação dos tipo de implementação. O utilizador tem de fechar o ficheiro executável está em execução (ou pode ser fechado automaticamente para implementações com um objetivo necessário) antes da implantação tipo pode ser instalado.

### <a name="try-it-out"></a>Faça um teste.

1.  Nas propriedades de um tipo de implementação do Configuration Manager, escolha o **comportamento instalar** separador.
2.  Escolher **adicionar** para adicionar um ou mais nomes de ficheiro executável que pretende procurar. Também pode adicionar um nome a apresentar para que seja mais fácil para os utilizadores a identificar aplicações na lista.
3.  Se a implementação irá ter um objetivo de necessária, o Assistente de implementação de software, opcionalmente, pode optar por **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação**.

Se a aplicação foi implementada como **disponível**e um utilizador final tenta instalar uma aplicação, será solicitado a eles para fechar a quaisquer especificou antes que eles podem continuar a instalação de executáveis em execução.

Se a aplicação foi implementada como **necessários**e a opção **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação** é selecionado, verá uma caixa de diálogo que informa de que os executáveis que especificou serão fechados automaticamente quando é atingido o prazo de instalação do aplicativo. Pode agendar essas caixas de diálogo **definições de cliente** > **agente do computador**. Se não pretender que o utilizador final para ver estas mensagens, selecione **ocultar no Centro de Software e em todas as notificações** sobre o **experiência do usuário** separador de propriedades da implementação.

Se a aplicação foi implementada como **necessários** e a opção **fechar automaticamente quaisquer executáveis em execução que especificou no separador de comportamento de instalação da caixa de diálogo de propriedades de tipo de implementação** não é em seguida, selecionado, a instalação da aplicação irá falhar se uma ou mais das aplicações especificadas estão em execução.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Criar certificados PFX com o suporte de S MIME

Agora pode criar um perfil de certificado PFX que suporta S/MIME e implementá-la aos utilizadores.  Este certificado, em seguida, pode ser utilizado para encriptação S/MIME e desencriptação em todos os dispositivos que o utilizador tiver inscrito.

Além disso, pode agora especificar várias autoridades de certificação (AC) em várias funções de sistema de sites de ponto de registo de certificados e, em seguida, atribuir quais solicitações de processo do ACS como parte do perfil de certificado.

Para dispositivos iOS, pode associar um perfil de certificado PFX para um perfil de e-mail e ativar a encriptação S/MIME.  Em seguida, isso permite que o S/MIME no cliente de e-mail nativa no iOS e associa o certificado de encriptação S/MIME correto para o mesmo.

Para obter mais informações sobre os certificados no Configuration Manager, consulte [introdução aos perfis de certificado no System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Novas definições de conformidade para dispositivos iOS

Adicionámos novas definições que pode utilizar nos seus itens de configuração para dispositivos iOS. Estas são as definições que já existiam no Microsoft Intune numa configuração autónoma e estão agora disponíveis ao utilizar o Intune com o Configuration Manager. Se precisar de ajuda com qualquer uma destas definições, consulte [definições de política do iOS no Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Dados de sincronização de aplicações geridas para o iCloud**
- **Handoff continue as atividades noutro dispositivo**
- **Partilha de fotografias em iCloud**
- **Fototeca em iCloud**
- **Confiar em novos autores de aplicações empresariais**
- **Permitir que o utilizador transfira conteúdos da Ibooks store sinalizados como "Erótico"** (modo supervisionado apenas)
- **Força Apple emparelhados a utilizar deteção no pulso**
- **Palavra-passe para AirPlay a enviar pedidos**
- **Modificar as definições de conta** (modo supervisionado apenas)
- **Alterações às definições de utilização de dados via rede móvel de aplicação** (modo supervisionado apenas)
- **Apagar todo o conteúdo e definições** (modo supervisionado apenas)
- **Configurar restrições no dispositivo** (modo supervisionado apenas)
- **Utilize emparelhamento de anfitriões para controlar os dispositivos com um dispositivo iOS pode emparelhar** (modo supervisionado apenas)
- **Instalar certificados e perfis de configuração** (modo supervisionado apenas)
- **Modificação do nome do dispositivo** (modo supervisionado apenas)
- **Modificação do código de acesso** (modo supervisionado apenas)
- **O emparelhamento do Apple Watch** (modo supervisionado apenas)
- **Modificação das definições de notificação** (modo supervisionado apenas)
- **Modificação da imagem de fundo** (modo supervisionado apenas)
- **Modificação de definições de submissão de diagnósticos** (modo supervisionado apenas)
- **Modificação de Bluetooth** (modo supervisionado apenas)
- **AirDrop** (modo supervisionado apenas)
- **Utilizar a Siri para consultar conteúdos gerados pelo utilizador da Internet** (modo supervisionado apenas)
- **Filtro de palavras ofensivas da Siri** (modo supervisionado apenas)
- **Devolver resultados da Internet na pesquisa Spotlight** (modo supervisionado apenas)
- **Pesquisa de definição de palavras** (modo supervisionado apenas)
- **Teclados preditivos** (modo supervisionado apenas)
- **Correção automática** (modo supervisionado apenas)
- **Verificação ortográfica do teclado** (modo supervisionado apenas)
- **Atalhos de teclado** (modo supervisionado apenas) <!--- - **Enterprise app trust settings modification** --->
- **Instalar aplicações com o Apple Configurator e o iTunes apenas** (modo supervisionado apenas)
- **Transferências automáticas de aplicações** (modo supervisionado apenas)
- **Efetuar alterações às definições da aplicação Find My Friends** (modo supervisionado apenas)
- **Acesso à iBooks store** (modo supervisionado apenas)
- **Aplicação mensagens** (modo supervisionado apenas)
- **Podcasts** (modo supervisionado apenas)
- **Apple Music** (modo supervisionado apenas)
- **iTunes Radio** (modo supervisionado apenas)
- **Apple News** (modo supervisionado apenas)
- **Centro de jogos** (modo supervisionado apenas)
- **Tratar o AirDrop como um destino não gerido**

## <a name="android-for-work-support"></a>Android para o suporte de trabalho

A partir da Technical Preview versão 1702, é possível ligar uma conta do Google para o seu inquilino MDM híbrida. Isto permite-lhe fazer o seguinte:

- Inscrever [Android dispositivos suportados](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) como Android for Work, a criação de perfis de trabalho nos dispositivos inscritos
- Aprove aplicações na Play for Work store, sincronizá-los com a consola do Configuration Manager e, em seguida, implementá-las para perfis de trabalho dos dispositivos
- Criar e implementar itens de configuração para configurar definições de perfil e a palavra-passe de trabalho para esses dispositivos
- Criar e implementar perfis de acesso de recursos e itens de política de conformidade para Android para dispositivos de trabalho tal como já para dispositivos Android
- Executar a eliminação seletiva em dispositivos Android para dispositivos de trabalho

Quando inscreve um dispositivo como Android for Work cria um perfil de trabalho no dispositivo quais o Intune pode gerir. Este perfil de trabalho existe lado a lado com o perfil pessoal no dispositivo Android. Os usuários podem alternar facilmente entre aplicações de perfil de trabalho e aplicações do perfil pessoal. Não é possível gerir itens no perfil pessoal. Aplicações e dados pessoais permanecem não geridos. Configuration Manager tem controlo total sobre o perfil de trabalho e os respetivos conteúdos e pode removê-lo do dispositivo.

O Android for Work é uma plataforma separada do Android, e terá de decidir que formulário da gestão a utilizar para dispositivos Android que suportem perfis de trabalho.

### <a name="try-it-out"></a>Experimente!
As secções seguintes descrevem Android para gestão de trabalho.

#### <a name="enable-android-for-work-management"></a>Ativar o Android para gestão de trabalho
1. Criar uma conta Google no https://accounts.google.com/SignUp para utilizar como do Android para a conta de administrador de trabalho que será associada a todos os Android para tarefas de gestão de trabalho para este inquilino do Intune. Isto pode ser uma conta Google partilhada entre os administradores que gerem os dispositivos Android. Esta é a conta Google que sua organização utiliza para gerir e publicar aplicações na consola Play for Work. Irá utilizar esta conta para aprovar as aplicações na Play Store de trabalho, portanto, mantenha um registo de nome da conta e palavra-passe.
2. Ative a inscrição de dispositivos Android ao vincular a conta Google para o inquilino do Intune gerenciado no Configuration Manager:
   1. Aceda a **Administration** > **descrição geral** > **serviços Cloud** > **subscrições do Microsoft Intune**  e selecione a sua subscrição do Intune.
   2. No Friso, clique em **configurar plataformas** > **Android** e certifique-se **ativar inscrição Android** está marcada.
   3. No Friso, clique em **configurar plataformas** > **Android for Work**.
   4. Na caixa de diálogo, clique em **configurar o Android for Work na consola do Intune**. Abre a consola do Intune no seu browser.
   5. Utilize as credenciais de administrador do Intune para iniciar sessão no portal do Intune.
   6. Clique em **configurar** para abrir o Google Play site Android for Work.
   7. Da Google início de sessão na página, introduza as credenciais da conta Google a partir do passo 1 e, em seguida, forneça as informações da sua empresa.
3. Quando regressar ao portal do Intune, o Android for Work está ativado e tem três opções de inscrição do Android para dispositivos de trabalho:
   - **Gerir todos os dispositivos como Android** – (desativado) todos os dispositivos Android, incluindo os dispositivos que suportam o Android for Work, serão inscritos como dispositivos Android convencionais
   - **Gerir dispositivos suportados como Android for Work** – (ativado) todos os dispositivos que suportam o Android for Work são inscritos como Android para dispositivos de trabalho. Todos os dispositivos Android que não suportam o Android for Work é inscrito como um dispositivo Android convencional.
   - **Gerir dispositivos suportados para utilizadores apenas nestes grupos como Android for Work** -(teste) permite-lhe direcionar a Android para gestão de trabalho a um conjunto limitado de utilizadores. Apenas os membros destes grupos selecionados que inscrevam um dispositivo que suporte o Android for Work são inscritos como Android para dispositivos de trabalho. Todos os outros dispositivos são inscritos como dispositivos Android.
  
> [!NOTE]
> Um problema conhecido impede que o **gerir dispositivos suportados para utilizadores apenas nestes grupos como Android for Work** opção de funcionar conforme esperado. Os dispositivos dos utilizadores no Azure AD especificado serão inscritos de grupos como Android, em vez do Android for Work. Para testar o Android for Work, tem de utilizar o **gerir todos os dispositivos suportados como Android for Work**.


  Para habilitar o Android para a inscrição de trabalho, tem de escolher uma das opções na parte inferior dois. O **gerir dispositivos suportados para utilizadores apenas nestes grupos como Android for Work** opção exige que tem de definir primeiro os grupos de segurança do Azure Active Directory.

Verá o nome da conta e o nome de organização no portal do Intune quando a ligação estiver concluída; nessa altura, pode fechar ambos os navegadores.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar o Android for Work
Siga estes passos para aprovar as aplicações na Play Store de trabalho, sincronizá-las para a consola do Configuration Manager e implementá-las em gerenciado dispositivos Android for Work. Para implementar aplicações para perfis de trabalho dos utilizadores, terá de aprovar as aplicações na Play for Work e, em seguida, sincronize as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.
2. Inicie sessão com a conta de administrador do Google vinculada ao seu inquilino do Intune.
3. Procurar aplicações que pretende implementar no seu ambiente e clique em **aprovar** para cada uma delas.
4. Na consola do Configuration Manager, aceda a **administrador** > **descrição geral** > **serviços Cloud**  >  **Android for Work** e clique em **sincronização**.
5. Aguarde até 10 minutos para as aplicações sincronizar e, em seguida, aceda **biblioteca de Software** > **descrição geral** > **gestão de aplicações**  >  **Licença informações para aplicações de Store**.
6. Clique numa aplicação sincronizada do Play for Work e, em seguida, clique em **Criar aplicação**.
7. Conclua o assistente e clique em **fechar**.
8. Aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicativos**, selecione um aplicações Android for Work e implementar como de costume.

Sincronizar Play para aplicações de trabalho com o Configuration Manager, terá de aprovar a pelo menos uma aplicação na Play para o Web site de trabalho.

#### <a name="enroll-an-android-for-work-device"></a>Inscrever um dispositivo Android for Work
Como inscrever dispositivos Android para dispositivos de trabalho é semelhante a inscrição para Android. Transfira e execute a aplicação Portal da empresa para Android no dispositivo móvel. Será solicitado a criar um perfil de trabalho como parte do processo de inscrição.  Depois de criar o perfil de trabalho, tem de mudar para a versão gerida do Portal da empresa. O Portal da empresa gerido é identificado com uma pequeno mala laranja no canto inferior direito.

#### <a name="create-and-deploy-a-configuration-item"></a>Criar e implementar um item de configuração
O Android for Work tem dois grupos de definições para itens de configuração:
- Palavra-passe
- Perfil de trabalho

Pode configurar o conteúdo de partilha entre perfis de trabalho, bem como os seguintes itens de configuração em dispositivos com Android 6 ou superior:
- O comportamento para solicitar permissões específicas de aplicações
- Se as notificações para aplicações no perfil de trabalho são visíveis no ecrã de bloqueio

Para experimentar, criar um item de configuração no fluxo de trabalho padrão, escolha **Android for Work** sobre o **geral** página e configurar as definições para cada um dos grupos de definições, adicionar o item de configuração para uma linha de base e implementar como de costume. Estas definições só serão aplicadas a dispositivos inscritos como Android for Work e não as inscritos como Android.

#### <a name="perform-selective-wipe"></a>Executar a eliminação seletiva
Os dispositivos inscritos como Android for Work pode apenas ser apagado seletivamente porque apenas a gerir o perfil de trabalho. Esta ação protege o perfil pessoal que está a ser apagado. Efetuar uma eliminação seletiva num dispositivo Android for Work remove o perfil de trabalho, incluindo todas as aplicações e dados e anular a inscrição do dispositivo.

A eliminação seletiva de um dispositivo Android for Work, utilize o normal [processo de eliminação seletiva](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) na consola do Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problemas conhecidos para Android for Work
**Configurar a sincronização agendar no Android as causas de perfis de e-mail de trabalho-los para conseguir implementar** uma das opções na IU do ConfigMgr para Android para perfis de e-mail de trabalho é "Agenda". Em outras plataformas, isso permite que o administrador configurar uma agenda para a sincronização de e-mail e outros dados de conta de e-mail para os dispositivos móveis que for implementado. No entanto, ele não funciona para Android para perfis de e-mail de trabalho e escolher qualquer opção que não seja "Não configurada" fará com que o perfil a não ser implementada para todos os dispositivos.
