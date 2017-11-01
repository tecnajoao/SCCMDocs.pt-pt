---
title: "Configurar a sua subscrição com o Lookout"
titleSuffix: Configuration Manager
description: "Este tópicos fornece detalhes sobre como configurar a proteção contra ameaças do Lookout dispositivo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 142926bc41a79adc8d8300e413022fb0e3566c5a
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configurar a sua subscrição para proteção contra ameaças do Lookout dispositivo

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para preparar a sua subscrição para o serviço de proteção de ameaças de dispositivo Lookout, suporte de Lookout (enterprisesupport@lookout.com) tem as seguintes informações sobre a sua subscrição do Azure Active Directory (Azure AD). O inquilino de segurança de ponto final de mobilidade Lookout será associado a sua subscrição do Azure AD para integrar o Lookout com o Intune. 

* **ID de inquilino do Azure AD**
* **ID de objeto de grupo do Azure AD** para **completa** o acesso à consola Lookout
* **ID de objeto de grupo do Azure AD** para **restrito** Lookout acesso à consola (opcional)

> [!IMPORTANT]
> Não é possível utilizar um inquilino de segurança de ponto final de Mobile Lookout existente que já não está associado ao inquilino do Azure AD para a integração com o Azure AD e o Intune. Contacte o suporte de Lookout para criar um novo inquilino de segurança de ponto final do Lookout Mobile. Utilize o novo inquilino para carregar os utilizadores do Azure AD.

Utilize a secção seguinte para recolher as informações que necessárias para lhe dar à equipa de suporte de Lookout.  

## <a name="get-your-azure-ad-information"></a>Obter as informações do Azure AD
### <a name="azure-ad-tenant-id"></a>ID de inquilino do Azure AD
Iniciar sessão para o [portal de gestão do Azure AD](https://manage.windowsazure.com) e selecione a sua subscrição. 

![captura de ecrã da página do Azure AD que mostra o nome do inquilino](media/aad_tenant_name.png) quando escolher o nome da sua subscrição, o URL resultante inclui o ID da subscrição.  Se tiver algum problema ao localizar o seu ID de subscrição, consulte este [artigo de suporte da Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) para dicas sobre ao localizar o seu ID de subscrição.   
### <a name="azure-ad-group-id"></a>ID de grupo do Azure AD
A consola Lookout suporta 2 níveis de acesso:  
* **Acesso total:** O administrador do Azure AD, pode criar um grupo de utilizadores que têm acesso total e, opcionalmente, criar um grupo de utilizadores que terão acesso restrito.  Apenas os utilizadores nestes grupos conseguirá iniciar sessão para o **consola Lookout**.
* **Acesso restrito:** Os utilizadores deste grupo terão sem acesso a vários configuração e inscrição relacionadas com módulos da consola Lookout e têm acesso só de leitura para o **política de segurança** módulo da consola Lookout.  

Para obter mais detalhes sobre as permissões, leia o artigo [neste artigo](https://personal.support.lookout.com/hc/en-us/articles/114094105653) no Web site da Lookout.

O **ID de objeto de grupo** no **propriedades** página do grupo no **consola de gestão do Azure AD**.

![captura de ecrã da página de propriedades com o campo de GroupID realçado](media/aad_group_object_id.png)

Assim que recolhemos estas informações, contacte o suporte de Lookout (e-mail: enterprisesupport@lookout.com).

O suporte de lookout irá trabalhar com o seu contacto principal para carregar a sua subscrição e criar a sua conta de empresa Lookout, utilizando as informações que recolheu.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configurar a subscrição com a proteção contra ameaças do Lookout dispositivo
### <a name="step-1-set-up-your-device-threat-protection"></a>Passo 1: Configurar a proteção contra ameaças do dispositivo
Depois do suporte de Lookout cria a conta de empresa Lookout, pode iniciar sessão na consola de Lookout.   É enviado um e-mail de Lookout para contacto principal da sua empresa com uma ligação para o url de início de sessão: https://aad.lookout.com/les?action=consent

Tem de utilizar uma conta de utilizador com a função do Azure AD de Administrador Global quando que primeiro inicie sessão consola do Lookout, uma vez que o Lookout necessita que esta informação para registar o inquilino do Azure AD.   Início de sessão subsequente serão requer que o utilizador tem este nível de privilégio do Azure AD.  Neste primeiro início de sessão, é apresentada uma página de consentimento. Escolha **aceitar** para concluir o registo.

![captura de ecrã da primeira página de início de sessão de tempo da consola Lookout](media/lookout-initial-login.png)

Assim que aceite e autorizado, são redirecionados para a consola Lookout. Inícios de sessão subsequentes após o registo inicial pode ser feito utilizando o URL: https://aad.lookout.com

Consulte o [artigo de resolução de problemas]() caso se depare com problemas de início de sessão.

Os passos seguintes descrevem as tarefas que terá de efetuar para concluir o Lookout configurar dentro de [Lookout consola](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Passo 2: Configurar o conector do Intune

1.  Na consola do Lookout, do **sistema** módulo, escolha o **conectores** separador e selecione **Intune**.

  ![captura de ecrã da consola Lookout o separador de conectores abrir e, opção Intune realçado](media/lookout-setup-intune-connector.png)

2.  A opção de definições de ligação, configure a frequência de heartbeat em minutos.  O conector do Intune agora está pronto.  

  ![captura de ecrã do separador de definições de ligação com a frequência de heartbeat configuradas a mostrar](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Passo 3: Configurar grupos de inscrição
No **inscrição gestão** opção, definir um conjunto de utilizadores cujos dispositivos devem estar inscrito no Lookout. A melhor prática é começar a utilizar um pequeno grupo de utilizadores para testar e se familiarize com como funciona a integração.  Quando estiver satisfeito com os resultados do teste, pode expandir a inscrição para os grupos adicionais de utilizadores.

Para começar com grupos de inscrições, defina primeiro um grupo de segurança do Azure AD que seria um boa primeiro conjunto de utilizadores para se inscrever na proteção contra ameaças do Lookout dispositivo. Assim que tiver o grupo criado no Azure, AD, na consola do Lookout, vá para o **inscrição gestão** opção e adicione o grupo de segurança do Azure AD **apresentar nomes** para inscrição.

Quando um utilizador é um grupo de inscrição, qualquer um dos respetivos dispositivos que são identificados e suportados no Azure AD são elegíveis para ativação na proteção contra ameaças do Lookout dispositivo e inscritos.  Na primeira vez que abrem o Lookout para a aplicação de trabalho nos respetivos dispositivos suportados, o dispositivo está ativado no Lookout.

![captura de ecrã da página de inscrição do conector do Intune](media/lookout-enrollment.png)

A melhor prática consiste em utilizar a predefinição (5 minutos) para o incremento de tempo para verificar a existência de novos dispositivos.

>[!IMPORTANT]
> O nome a apresentar é sensível às maiúsculas e minúsculas.  Utilize o **nome a apresentar** conforme mostrado no **propriedades** página do grupo de segurança no portal do Azure. Tenha em atenção na imagem abaixo que o **propriedades** página do grupo de segurança, o nome a apresentar é camel case.  No entanto, o título é apresentado em todos os minúsculas e não deve ser utilizado para introduzir na consola do Lookout.
>![captura de ecrã do portal do Azure, o serviço de Azure Active Directory, a página de propriedades](media/aad-group-display-name.png)

A versão atual tem as seguintes limitações:  
* Não há nenhuma validação para os nomes a apresentar o grupo.  Certifique-se de que utiliza o valor no **nome a apresentar** campo apresentado no portal do Azure para o grupo de segurança do Azure AD.
* Criar grupos de grupos não é atualmente suportado.  Grupos de segurança do Azure AD especificada só pode conter utilizadores e grupos não aninhados.


### <a name="step-4-configure-state-sync"></a>Passo 4: Configurar a sincronização de estado
No **sincronização de estado** opção, especifique o tipo de dados que devem ser enviados para o Intune.  Atualmente, tem de ativar o estado do dispositivo e o estado de ameaça por ordem para a integração do Lookout Intune funcione corretamente.  Estas estão ativadas por predefinição.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Passo 5: Configurar informações de destinatários de e-mail de relatório de erro
No **erro gestão** opção, introduza o endereço de correio eletrónico que deve receber os relatórios de erros.

![captura de ecrã da página Gestão de erro de conector do Intune](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Passo 6. Configurar definições de inscrição
No **sistema** módulo, o **conectores** página, especifique o número de dias antes de um dispositivo é considerado como desligada.  Dispositivos desligados são considerados como não conformes e serão impedidos de aceder a aplicações da empresa com as políticas de acesso condicional do SCCM. Pode especificar valores entre 1 e 90 dias.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Passo 7: Configurar notificações por e-mail
Se pretende receber alertas de e-mail para ameaças, inicie sessão no [consola Lookout](https://aad.lookout.com) com a conta de utilizador que deve receber as notificações. No **preferências** separador do **sistema** módulo, escolha as notificações pretendidas e configure-os **ON**. Guarde as alterações.

![captura de ecrã da página de preferências com a conta de utilizador apresentada](media/lookout-email-notifications.png) se já não pretender receber notificações por e-mail, como as notificações **OFF** e guarde as alterações.
### <a name="step-8-configure-threat-classification"></a>Passo 8: Configurar a classificação de ameaça
Proteção contra ameaças do lookout dispositivo classifica móveis ameaças de vários tipos. O [classificações de ameaça Lookout](http://personal.support.lookout.com/hc/en-us/articles/114094130693) têm níveis de risco predefinidos associados aos mesmos. Estes podem ser alteradas em qualquer altura para suite requisitos da sua empresa.

![captura de ecrã da página de política que mostra ameaça e classificações](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Os níveis de risco especificado que aqui são um aspeto importante de proteção contra ameaças do dispositivo, porque a integração do Intune calcula a conformidade do dispositivo, de acordo com estes níveis de risco no tempo de execução. Por outras palavras, o administrador do Intune define uma regra de política para identificar um dispositivo como não conforme se o dispositivo tem uma ameaça Active Directory com um mínimo ao nível do: alta, média ou baixa. A política de classificação de ameaça na proteção contra ameaças do Lookout dispositivo unidades diretamente o cálculo de conformidade do dispositivo no Intune.

## <a name="watching-enrollment"></a>Observar inscrição
Assim que a configuração estiver concluída, proteção contra ameaças do Lookout dispositivo é iniciado consultar o Azure AD para dispositivos que correspondem aos grupos de inscrição especificado.  Pode encontrar informações sobre os dispositivos inscritos no módulo de dispositivos.  O estado inicial de dispositivos é mostrado como pendente.  As alterações de estado de dispositivo depois do Lookout for Work aplicação é instalada, abrir e ativado no dispositivo.  Para obter mais informações sobre como obter o Lookout para a aplicação de trabalho instalada no dispositivo, consulte o [configurar e implementar o Lookout para aplicações de trabalho](configure-and-deploy-lookout-for-work-apps.md) tópico.
## <a name="next-steps"></a>Passos seguintes
[Ativar ligação Lookout MTP Intune](enable-lookout-connection-in-intune.md)
