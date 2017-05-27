---
title: "Proteger aplicações ao utilizar políticas de gestão de aplicações móveis | Documentos do Microsoft"
description: "Modificar a funcionalidade das aplicações que implementa, de modo que irão cumprir a conformidade da empresa e as políticas de segurança."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 74f4dd44089d4a13526c981589e1f497f0e10290
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Proteger aplicações através de políticas de gestão de aplicações móveis no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Políticas de gestão de aplicações do System Center Configuration Manager permitem-lhe modificar a funcionalidade das aplicações que implementa para ajudar a colocá-los em linha com a sua empresa políticas de segurança e conformidade. Por exemplo, pode restringir operações de corte, cópia e colagem numa aplicação restrita ou configurar uma aplicação para abrir todos os URLs num browser gerido. Suporte para políticas de gestão de aplicações:  

-   Dispositivos a executar o Android 4 e posterior  

-   Dispositivos que executem iOS 7 e versões posteriores  

Também pode utilizar as políticas de gestão de aplicações móveis para proteger as aplicações em dispositivos que não são geridos pelo Intune. Utilizar esta nova funcionalidade, pode aplicar políticas de gestão de aplicações móveis a aplicações de ligar para serviços do Office 365. Não é suportada para aplicações que estabelecem ligação no local para o Exchange ou do SharePoint.  

Para utilizar esta nova funcionalidade, terá de utilizar o portal de pré-visualização Azure. Os tópicos seguintes podem ajudá-lo a familiarizar-se:  
-   [Introdução às políticas de gestão de aplicações móveis no portal do Azure](https://technet.microsoft.com/library/mt627830.aspx)  
-   [Criar e implementar políticas de gestão de aplicações móveis com o Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

 Não implemente uma política de gestão de aplicações diretamente como fazê-lo com itens de configuração e linhas de base no Configuration Manager. Em vez disso, associa a política ao tipo de implementação da aplicação que pretende restringir. Quando o tipo de implementação de aplicação é implementado e instalado em dispositivos, as definições que especifica em vigor.  

Para aplicar restrições a uma aplicação, a aplicação tem de incorporar o Microsoft Intune App Software Development Kit (SDK). Existem dois métodos para obter este tipo de aplicação:  

-   **Utilizar uma aplicação gerida por política** (Android e iOS): Estas aplicações tem a aplicação SDK incorporada. Para adicionar este tipo de aplicação, especifique uma ligação para a aplicação a partir de uma loja de aplicações, como o iTunes ou o Google Play. Não é necessário processamento adicional para este tipo de aplicação. Para obter uma lista de aplicações geridas por política que estão disponíveis para dispositivos iOS e Android, veja [Aplicações geridas para as políticas de gestão de aplicações móveis do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn708489.aspx).  

-   **Utilizar uma aplicação "encapsulada"** (Android e iOS): Estas aplicações são empacotadas novamente para incluir o SDK da aplicação ao utilizar o **Microsoft Intune App Wrapping Tool**. Normalmente esta ferramenta é utilizada para processar aplicações da empresa que foram criadas internamente. Não pode ser utilizada para processar aplicações que foram transferidas a partir da loja de aplicações. Consulte os artigos seguintes para obter mais informações:
    - [Preparar as aplicações iOS para a gestão de aplicações móveis com a ferramenta de encapsulamento de aplicações do Microsoft Intune](https://technet.microsoft.com/en-us/library/dn878028.aspx)

    - [Preparar as aplicações Android para gestão de aplicações móveis com a ferramenta de encapsulamento de aplicações do Microsoft Intune](https://technet.microsoft.com/en-us/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Criar e implementar uma aplicação com uma política de gestão de aplicações móveis  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Passo 1: Obter a ligação para uma aplicação gerida por política ou criar uma aplicação encapsulada  

-   **Para obter uma ligação para uma política de aplicação gerida por**: A partir da loja de aplicações, encontre e anote o URL da aplicação gerida por política que pretende implementar.  

     Por exemplo, o URL da aplicação Microsoft Word para iPad é **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Para criar uma aplicação encapsulada**: Utilize as informações nos tópicos [preparar as aplicações iOS para a gestão de aplicações móveis com o Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/dn878028.aspx) e [aplicações Prepare Android para gestão de aplicações móveis com o Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/en-us/library/mt147413.aspx) para criar uma aplicação encapsulada.  

     A ferramenta cria uma aplicação processada e um ficheiro de manifesto associado. Utilizar estes ficheiros quando cria uma aplicação do Configuration Manager que contém a aplicação.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Passo 2: Criar uma aplicação do Configuration Manager que contém uma aplicação  
 O procedimento para criar a aplicação do Configuration Manager é diferente consoante está a utilizar uma aplicação gerida por política (ligação externa), ou uma aplicação que foi criada utilizando a ferramenta de encapsulamento de aplicações do Microsoft Intune para iOS (pacote de aplicação para iOS). Utilize um dos seguintes procedimentos para criar a aplicação do Configuration Manager.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  No **base** separador o **criar** grupo, selecione **Criar aplicação** para abrir o **Criar aplicação** assistente.  

4.  Na página **Geral** , selecione **Detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

5.  Na lista pendente **Tipo**, selecione **Pacote de aplicação para iOS (ficheiro \*.ipa)**.  

6.  Escolher **procurar** para selecionar o pacote de aplicação que pretende importar e, em seguida, selecione **seguinte**.  

7.  Na página **Informações Gerais** , introduza o texto descritivo e as informações sobre a categoria que pretende que os utilizadores vejam no portal da empresa.  

8.  Conclua o assistente.  

 A nova aplicação é apresentada no nó **Aplicações** da área de trabalho **Biblioteca de Software** .  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Criar uma aplicação que contém uma ligação para uma aplicação gerida por política  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  No **base** separador o **criar** grupo, selecione **Criar aplicação** para abrir o **Criar aplicação** assistente.  

4.  Na página **Geral** , selecione **Detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

5.  Na lista pendente **Tipo** , selecione um dos seguintes:  

    -   IOS: **Pacote de aplicação para iOS da App Store**  

    -   Para Android: **Pacote de aplicação para Android no Google Play**  

6.  Introduza o URL da aplicação (a partir do passo 1) e, em seguida, selecione **seguinte**.  

7.  Na página **Informações Gerais** , introduza o texto descritivo e as informações sobre a categoria que pretende que os utilizadores vejam no portal da empresa.  

8.  Conclua o assistente.  

 A nova aplicação é apresentada no nó **Aplicações** da área de trabalho **Biblioteca de Software** .  

##  <a name="step-3-create-an-application-management-policy"></a>Passo 3: Criar uma política de gestão de aplicações  
 Em seguida, crie uma política de gestão de aplicações que associar a aplicação. Pode criar uma política de browser gerido ou geral.  

1)  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **políticas de gestão de aplicações**.  

2)  No **base** separador o **criar** grupo, selecione **criar política de gestão de aplicações**.  

3)  No **geral** página, introduza o nome e descrição para a política e, em seguida, selecione **seguinte**.  

4)  No **tipo de política** página, selecione a plataforma e o tipo de política para esta política e, em seguida, selecione **seguinte**. Estão disponíveis os seguintes tipos de política:  

-   **Geral**: O tipo de política gerais permite-lhe modificar a funcionalidade de aplicações que implementa para ajudar a colocá-los em linha com a sua conformidade da empresa e as políticas de segurança. Por exemplo, pode restringir as operações de corte, cópia e colagem numa aplicação restrita.  

-   **Browser gerido**: A política de Browser gerido permite-lhe decidir se pretende permitir ou bloquear o browser gerido de abrir uma lista de URLs. A política de Browser Gerido permite modificar a funcionalidade da aplicação Intune Managed Browser. É um browser que lhe permite gerir as ações que os utilizadores podem realizar, incluindo os sites que podem visitar e como são abertas as ligações para conteúdo no browser. Saiba mais sobre a  [aplicação Intune Managed Browser para iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) e a [aplicação Intune Managed Browser para Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  No **política para iOS** ou **política Android** página, configure os seguintes valores conforme necessário e, em seguida, selecione **seguinte**. As opções podem variar dependendo do tipo de dispositivo para o qual está a configurar a política.  

|Valor|Mais informações|  
|-----------|----------------------|  
|**Restringir o conteúdo Web a apresentar num browser gerido pela empresa**|Permite que todas as ligações na aplicação para abrir no Browser gerido. Para esta opção funcionar, esta aplicação tem de estar implementada em dispositivos.|  
|**Impedir cópias de segurança de Android** ou **Impedir cópias de segurança de iTunes e iCloud**|Desativa a cópia de segurança de informações da aplicação.|  
|**Permitir que a aplicação transfira dados para outras aplicações**|Especifica as aplicações para as quais esta aplicação pode enviar dados. Pode optar por não permitir a transferência de dados para qualquer aplicação, apenas permitir a transferência para outras aplicações restritas ou permitir a transferência para qualquer aplicação.<br /><br /> Em dispositivos iOS, para impedir a transferência de documentos entre aplicações geridas e não geridas, também tem de configurar e implementar uma política de segurança de dispositivos móveis que desativa a definição **Permitir documentos geridos noutras aplicações não geridas**.<br /><br /> Se selecionar para apenas permitir a transferência para outras aplicações restritas, os Intune PDF e imagem visualizadores (se estiverem implementados) serão utilizados para abrir conteúdos dos respetivos tipos.|  
|**Permitir que a aplicação receba dados de outras aplicações**|Especifica de que aplicações esta aplicação pode receber dados. Pode optar por não permitir a transferência de dados a partir de qualquer aplicação, apenas permitir a transferência de outras aplicações restritas ou permitir a transferência de qualquer aplicação.|  
|**Impedir "Guardar Como"**|Desativa a utilização do **guardar como** opção em qualquer aplicação que utiliza esta política.|  
|**Restringir as operações de corte, cópia e colagem com outras aplicações**|Especifica como as operações de corte, cópia e colagem podem ser utilizadas com a aplicação. Escolha entre:<br /><br /> **Bloqueado** – não permitir operações de corte, cópia e colagem entre esta aplicação e outras aplicações.<br /><br /> **Aplicações geridas por política** – permite cortar, copiar e colar operações entre apenas esta aplicação e outras aplicações restritas.<br /><br /> **Aplicações geridas por política com colar em** – permite que os dados que tem cortados ou copiados desta aplicação apenas sejam colados noutras aplicações restritas. Permite que os dados que são cortados ou copiados de qualquer aplicação sejam colados nesta aplicação.<br /><br /> **Qualquer aplicação** -sem restrições para cortar, copiar e colar as operações de ou para esta aplicação.|  
|**Exigir PIN simples para acesso**|Exige que o utilizador introduzir um PIN que especifica para utilizar esta aplicação. É pedido ao utilizador para configurar isto da primeira vez que executam a aplicação.|  
|**Número de tentativas antes de redefinição do PIN**|Especifica o número de tentativas de introdução do PIN que podem ser efetuadas antes do utilizador ter de redefinir o PIN.|  
|**Exigir credenciais da empresa para obter acesso**|Requer que o utilizador tem de introduzir as respetivas informações de início de sessão empresarias antes de poderem aceder a aplicação.|  
|**Exigir a conformidade do dispositivo com a política empresarial para acesso**|Permite que a aplicação a ser utilizado apenas quando o dispositivo não é desbloqueado por jailbreak ou rooting.|  
|**Verificar novamente os requisitos de acesso após (minutos)**|Especifica o período de tempo antes dos requisitos de acesso da aplicação serem novamente verificados após a aplicação for iniciada (no **tempo limite** campo).<br /><br /> No **período de tolerância Offline** campo, se o dispositivo estiver offline, especifica o período de tempo antes dos requisitos de acesso da aplicação serem novamente verificados.|  
|**Encriptar dados da aplicação**|Especifica que todos os dados que está associados esta aplicação é encriptados, incluindo os dados armazenados externamente, como os dados armazenados em cartões SD.<br /><br /> **Encriptação para iOS**<br /><br /> Para aplicações que estão associadas uma política de gestão de aplicações móveis do Configuration Manager, os dados são encriptados em descanso ao utilizar a encriptação de nível de dispositivo que é fornecida pelo sistema operativo. Isto é ativado através de um dispositivo de política de PIN tem de ser definida pelo administrador de TI. Quando for necessário um PIN, os dados são encriptados de acordo com as definições na política de gestão de aplicações móveis. Conforme indicado na documentação da Apple, [os módulos utilizados pelo iOS 7 têm a certificação FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Encriptação para Android**<br /><br /> Para aplicações que estão associadas uma política de gestão de aplicações móveis do Configuration Manager, a encriptação é fornecida pela Microsoft. Os dados são encriptados em sincronia durante operações de E/S de ficheiros, de acordo com a definição na política de gestão de aplicações móveis. As aplicações geridas no Android utilizam encriptação AES-128 no modo CBC ao utilizar as bibliotecas de criptografia da plataforma. O método de encriptação não tem certificação FIPS 140-2. Conteúdo no armazenamento do dispositivo será sempre encriptado.|  
    |**Bloquear captura de ecrã** (apenas dispositivos Android)|Especifica que as funcionalidades de captura de ecrã do dispositivo estão bloqueadas durante a utilização desta aplicação.|  

6)  No **Browser gerido** página, selecione se o browser gerido é permitido para abrir apenas URLs na lista ou para bloquear o browser gerido abra os URLs na lista e, em seguida, escolha **seguinte**.  
Para obter mais informações, consulte o artigo [utilizando o acesso à Internet gerir geridos políticas de browser](manage-internet-access-using-managed-browser-policies.md).  

7)  Conclua o assistente.  

 A nova política é apresentada no nó **Políticas de Gestão de Aplicações** da área de trabalho **Biblioteca de Software** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Passo 4: Associar a política de gestão de aplicações com um tipo de implementação  

 Quando é criado um tipo de implementação para uma aplicação que necessita de uma política de gestão de aplicações, o Configuration Manager reconhece este e pede-lhe para associar uma política de gestão de aplicações. Para o Browser gerido, são necessárias para associar a política de gerais e de Browser gerido. Para obter mais informações, consulte o artigo [criar aplicações](create-applications.md).  

> [!IMPORTANT]  
>  Se a aplicação já está a ser implementada, a implementação para o novo tipo de implementação falhará até que esta associação é efetuada. Pode fazer a associação em **Propriedades** da aplicação, no separador **Gestão de Aplicações** .  

> [!IMPORTANT]  
>  Para dispositivos que executem sistemas operativos anteriores ao iOS 7.1, as políticas associadas não são removidas quando a aplicação é desinstalada.  
>   
>  Se o dispositivo está a inscrição do Configuration Manager, as políticas não serão removidas das aplicações. As aplicações com políticas aplicadas reter as definições de política, mesmo depois da aplicação é desinstalada e instalada novamente.  

##  <a name="step-5-monitor-the-app-deployment"></a>Passo 5: Monitorizar a implementação da aplicação  
 Assim que criar e implementar uma aplicação que está associada uma política de gestão de aplicações móveis, pode monitorizar a aplicação e resolver os conflitos de política.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **descrição geral** > **implementações**.  

3.  Selecione a implementação que criou. Em seguida, no **base** separador, escolha **propriedades**.  

4.  No painel de detalhes para a implementação em **objetos relacionados**, escolha **políticas de gestão de aplicações**.  

 Para obter mais informações sobre a monitorização de aplicações, consulte o artigo [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Saiba como são resolvidos os conflitos de políticas  
 Quando existe um conflito de política de gestão de aplicações móveis na primeira implementação para o utilizador ou dispositivo, o valor de definição específico que está em conflito é removido da política implementada na aplicação. A aplicação utilizará um valor de conflito incorporado.  

 Quando existe um conflito de política de gestão de aplicações móveis em implementações posteriores na aplicação ou utilizador, o valor de definição específico que está em conflito não é atualizado na política de gestão de aplicações móveis, que é implementada na aplicação e a aplicação utiliza o valor existente para essa definição.  

 Nos casos em que o dispositivo ou o utilizador recebe duas políticas em conflito, aplica-se o comportamento seguinte:  

-   Se ainda tiver sido implementada uma política no dispositivo, as definições da política existente não são substituídas.  

-   Se nenhuma política já tiver sido implementada no dispositivo e forem implementadas duas definições em conflito, a predefinição incorporada no dispositivo é utilizada.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Ver uma lista de aplicações geridas por políticas disponíveis  
 Para obter uma lista da política de aplicações geridas que estão disponíveis para dispositivos iOS e Android, consulte o artigo [parceiros de aplicações do Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune-partners).  

