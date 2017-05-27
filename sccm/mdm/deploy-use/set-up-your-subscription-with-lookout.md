---
title: "Configurar a sua subscrição com atento | O System Center Configuration Manager"
description: "Este tópicos fornece detalhes sobre como configurar a proteção de ameaça atento dispositivo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: b777140c753e709f4048a30e63d8ae730d3e8723
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configurar a sua subscrição para a proteção de ameaça atento dispositivo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para obter a sua subscrição está preparado para o serviço de proteção de ameaça de dispositivo atento, suporte de atento (enterprisesupport@lookout.com) tem as seguintes informações sobre a sua subscrição do Azure Active Directory (Azure AD). O inquilino de segurança de ponto final de mobilidade atento será associado com a sua subscrição do Azure AD para integrar atento com o Intune. 

* **ID de inquilino do Azure AD**
* **ID de objeto de grupo do Azure AD** para **completa** acesso à consola de atento
* **ID de objeto de grupo do Azure AD** para **restrito** atento acesso à consola (opcional)

> [!IMPORTANT]
> Um inquilino atento Mobile Endpoint segurança existente que já não esteja associado com o seu inquilino do Azure AD não pode ser utilizado para a integração com o Azure AD e o Intune. Contacte o suporte de atento para criar um novo inquilino de segurança de ponto final do atento Mobile. Utilize o novo inquilino para carregar os utilizadores do Azure AD.

Utilize a secção seguinte para recolher as informações que necessárias para lhe dar para a equipa de suporte atento.  

## <a name="get-your-azure-ad-information"></a>Obter as informações do Azure AD
### <a name="azure-ad-tenant-id"></a>ID de inquilino do Azure AD
Início de sessão para o [portal de gestão do Azure AD](https://manage.windowsazure.com) e selecione a sua subscrição. 

![captura de ecrã da página do Azure AD que mostra o nome do inquilino](media/aad_tenant_name.png) quando escolher o nome da sua subscrição, o URL resultante inclui o ID de subscrição.  Se tiver problemas de localizar o ID de subscrição, consulte a seguinte [artigo do suporte da Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) para obter sugestões sobre como localizar o seu ID de subscrição.   
### <a name="azure-ad-group-id"></a>ID do grupo do Azure AD
A consola atento suporta 2 níveis de acesso:  
* **Acesso total:** O administrador do Azure AD pode criar um grupo de utilizadores que têm acesso total e, opcionalmente, criar um grupo de utilizadores que terão acesso restrito.  Apenas os utilizadores nestes grupos poderão iniciar sessão a **consola atento**.
* **Acesso restrito:** Os utilizadores neste grupo terão sem acesso a configuração de várias e inscrição relacionados com módulos da consola atento e com acesso só de leitura para a **política de segurança** módulo da consola atento.  

Para obter mais detalhes sobre as permissões, consulte o artigo [neste artigo](https://personal.support.lookout.com/hc/en-us/articles/114094105653) no Web site atento.

O **ID de objeto de grupo** está ativada a **propriedades** página do grupo no **consola de gestão do Azure AD**.

![captura de ecrã da página de propriedades com campo GroupID realçado](media/aad_group_object_id.png)

Assim que recolheram estas informações, contacte o suporte de atento (correio eletrónico: enterprisesupport@lookout.com).

O suporte de atento irá trabalhar com o contacto primário para carregar a sua subscrição e criar a sua conta de empresa atento, utilizando as informações que recolheu.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configurar a subscrição com a proteção de ameaça atento dispositivo
### <a name="step-1-set-up-your-device-threat-protection"></a>Passo 1: Configurar a proteção de ameaça do dispositivo
Depois de suporte atento cria a sua conta atento Enterprise, pode iniciar sessão na consola do atento.   É enviado um e-mail a partir do atento para o contacto principal da sua empresa com uma ligação para o url de início de sessão: https://aad.lookout.com/les?action=consent

Tem de utilizar uma conta de utilizador com a função do Azure AD de Administrador Global quando primeiro iniciar sessão na consola atento, uma vez que atento necessita que esta informação para registar o seu inquilino do Azure AD.   Início de sessão subsequentes não irá necessitar do utilizador tenha este nível de privilégio do Azure AD.  Neste primeiro início de sessão, é apresentada uma página de autorização. Escolher **aceitar** para concluir o registo.

![captura de ecrã da primeira página de início de sessão de tempo da consola atento](media/lookout-initial-login.png)

Depois de aceite e autorizado, é redirecionado para a consola atento. Inícios de sessão subsequentes após o registo inicial pode ser efetuado através do URL: https://aad.lookout.com

Consulte o [artigo de resolução de problemas]() caso se depare com problemas de início de sessão.

Os passos seguintes descrevem as tarefas que tem de efetuar para concluir o atento configurar dentro de [atento consola](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Passo 2: Configurar o conector do Intune

1.  Na consola do atento, a partir de **sistema** módulo, escolha o **conectores** separador e selecione **Intune**.

  ![captura de ecrã da consola atento com o separador de conectores abrir e opção Intune realçado](media/lookout-setup-intune-connector.png)

2.  A opção de definições de ligação, configure a frequência de heartbeat em minutos.  O conector do Intune agora está pronto.  

  ![captura de ecrã do separador de definições de ligação com a mostrar a frequência de heartbeat configurada](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Passo 3: Configurar grupos de inscrição
No **inscrição gestão** opção, definir um conjunto de utilizadores cujos dispositivos devem ser registados no atento. A melhor prática é começar com um pequeno grupo de utilizadores para testar e familiarize-se com como funciona a integração.  Assim que estiver satisfeito com os resultados de teste, pode expandir a inscrição para grupos adicionais de utilizadores.

Para começar a utilizar com grupos de inscrições, defina primeiro um grupo de segurança do Azure AD que seria um boa primeiro conjunto de utilizadores para se inscrever no proteção de ameaça atento dispositivo. Assim que tiver o grupo criado no Azure, AD, na consola do atento, vá para o **inscrição gestão** opção e adicione o grupo de segurança do Azure AD **nomes de apresentação** para a inscrição.

Quando um utilizador estiver num grupo de inscrição, qualquer um dos respetivos dispositivos que estão identificados e suportados no Azure AD estão inscritos e elegíveis para ativação em matéria de proteção de ameaça atento dispositivo.  Na primeira vez que abrirem o atento para a aplicação de trabalho no respetivo dispositivo suportado, o dispositivo se encontra ativado no atento.

![captura de ecrã da página de inscrição do conector do Intune](media/lookout-enrollment.png)

O procedimento recomendado é utilizar a predefinição (5 minutos) para o incremento de tempo para verificar a existência de novos dispositivos.

>[!IMPORTANT]
> O nome a apresentar é sensível a maiúsculas e minúsculas.  Utilize o **nome a apresentar** conforme mostrado no **propriedades** página do grupo de segurança no portal do Azure. Tenha em atenção na imagem abaixo que o **propriedades** página do grupo de segurança, o nome a apresentar é camel maiúsculas e minúsculas.  No entanto, o título é apresentado em todos os minúscula e não deve ser utilizado para introduzir a consola atento.
>![captura de ecrã do portal do Azure, o serviço do Azure Active Directory, a página de propriedades](media/aad-group-display-name.png)

A versão atual tem as seguintes limitações:  
* Não existe nenhuma validação para os nomes a apresentar o grupo.  Certifique-se que utilize o valor no **nome a apresentar** campo apresentado no portal do Azure para o grupo de segurança do Azure AD.
* Criar grupos no âmbito de grupos não é atualmente suportado.  Grupos de segurança do Azure AD especificado só pode conter utilizadores e grupos aninhados não.


### <a name="step-4-configure-state-sync"></a>Passo 4: Configurar a sincronização de estado
No **sincronização de estado** opção, especifique o tipo de dados que devem ser enviados para o Intune.  Atualmente, tem de ativar o estado do dispositivo e o estado de ameaça por ordem para a integração do Intune atento funcione corretamente.  Estas estão ativadas por predefinição.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Passo 5: Configurar informações de destinatário de correio eletrónico de relatório de erros
No **erro gestão** opção, introduza o endereço de correio eletrónico que deve receber os relatórios de erros.

![captura de ecrã da página de gestão de erro de conector do Intune](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Passo 6. Configurar definições de inscrição
No **sistema** módulo, no **conectores** página, especifique o número de dias antes de um dispositivo é considerado como desligada.  Dispositivos desligados são considerados como não conformidade e serão impedidos de aceder as aplicações da empresa com as políticas de acesso condicional do SCCM. Pode especificar valores entre 1 e 90 dias.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Passo 7: Configurar notificações por correio eletrónico
Se pretender receber alertas de correio eletrónico de ameaças, inicie sessão no [consola atento](https://aad.lookout.com) com a conta de utilizador que deve receber as notificações. No **preferências** separador do **sistema** módulo, escolha as notificações pretendidas e defini-las **ON**. Guarde as alterações.

![captura de ecrã da página de preferências com a conta de utilizador apresentada](media/lookout-email-notifications.png) se já não pretende receber notificações por correio eletrónico, configurar as notificações para **OFF** e guarde as alterações.
### <a name="step-8-configure-threat-classification"></a>Passo 8: Configurar classificação de ameaça
Proteção de ameaça de dispositivo atento classifica móveis ameaças de vários tipos. O [classificações de ameaça atento](http://personal.support.lookout.com/hc/en-us/articles/114094130693) têm níveis de risco predefinido associados aos mesmos. Estes podem ser alteradas em qualquer altura ao conjunto de aplicações requisitos da sua empresa.

![captura de ecrã da página que mostra ameaça e classificações de política](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Os níveis de risco especificado que aqui são um aspeto importante de proteção de ameaça de dispositivo, uma vez que a integração do Intune calcula conformidade do dispositivo, de acordo com estes níveis de risco no tempo de execução. Por outras palavras, o administrador do Intune define uma regra de política para identificar um dispositivo como não conformidade, se o dispositivo tem uma ameaça Active Directory com um mínimo nível de: alta, média ou baixa. A política de classificação de ameaça na proteção de ameaça de dispositivo atento unidades diretamente o cálculo de conformidade do dispositivo no Intune.

## <a name="watching-enrollment"></a>Observar inscrição
Assim que o programa de configuração estiver concluído, a proteção de ameaça de dispositivo atento inicia de consulta do Azure AD para dispositivos que correspondem aos grupos de inscrição especificado.  Pode encontrar informações sobre os dispositivos inscritos no módulo dispositivos.  O estado inicial para dispositivos será apresentado como pendente.  As alterações de estado do dispositivo instalado atento para a aplicação de trabalho, aberto e ativado no dispositivo.  Para obter detalhes sobre como obter o atento para trabalho aplicação instalada no dispositivo, consulte o [configurar e implementar atento para aplicações de trabalho](configure-and-deploy-lookout-for-work-apps.md) tópico.
## <a name="next-steps"></a>Passos seguintes
[Ativar atento MTP ligação do Intune](enable-lookout-connection-in-intune.md)

