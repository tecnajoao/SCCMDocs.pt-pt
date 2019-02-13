---
title: 'Como criar perfis VPN '
titleSuffix: Configuration Manager
description: Saiba como criar perfis VPN no System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8f00b3aef75d2200d991f99e514f83636f7b16bb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121816"
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Como criar perfis VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os tipos de ligação disponíveis para as plataformas de dispositivos diferentes são descritos nas [perfis VPN no System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

Para conexões de VPN de terceiros, distribua a aplicação VPN antes de implementar o perfil VPN. Se não implementar a aplicação, serão pedido aos utilizadores para fazê-lo quando o utilizador tentar estabelecer ligação à VPN. Para saber como implementar aplicações, veja [implementar aplicações com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Criar um perfil VPN   

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **definições de compatibilidade** > **acesso a recursos da empresa**  >  **Perfis VPN**.  

2. Na **home page** separador a **Create** de grupo, escolha **criar perfil VPN**.  


3. Concluir o **gerais** página. . Tenha em atenção o seguinte:  

   - Selecione o adequado **plataforma**.

      - Se selecionar a plataforma do Windows 8.1, tem a opção para selecionar **importar um item de perfil VPN existente de um ficheiro** para importar informações do perfil VPN que foi exportadas para um arquivo XML.

   - Utilize os carateres \\/:\*?&lt;>&#124; ou o caráter de espaço no nome do perfil VPN. Estes carateres não são suportados pelo perfil de VPN do Windows Server.  


4. Sobre o **ligação** , especifique:  

   - **Tipo de ligação**: Escolha o tipo de ligação de VPN. Pode escolher entre os tipos de ligação na tabela seguinte.  

   - **Lista de servidores**: Adicione um novo servidor a utilizar para a ligação VPN. Dependendo do tipo de ligação, pode adicionar um ou mais servidores VPN e especificar o servidor predefinido.  

     > [!NOTE]  
     >  Os dispositivos com o iOS não suportam a utilização de vários servidores VPN. Se configurar vários servidores VPN e, em seguida, implementar o perfil VPN num dispositivo iOS, só é utilizado o servidor predefinido.  

     Esta tabela fornece opções para tipos de ligação. Consulte a documentação do servidor VPN para obter mais informações.

| &nbsp;&nbsp;Opção&nbsp;&nbsp; | Mais informações | &nbsp;&nbsp;Ligação&nbsp;tipo&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Realm**     |O realm de autenticação que pretende utilizar. Um realm de autenticação é um agrupamento de recursos de autenticação que é utilizado pelo tipo de ligação Pulse Secure.|Pulse Secure|    
|**Função**        |A função de utilizador que tem acesso a esta ligação. |Pulse Secure|  
|**Grupo ou domínio de início de sessão** |O nome do grupo de início de sessão ou do domínio que deseja se conectar.|Dell SonicWALL Mobile Connect|  
|**Identificação digital**  |Uma cadeia, por exemplo "Contoso código de identificação digital" que será utilizado para verificar que o servidor VPN pode ser confiável.<br /><br /> Uma identificação digital pode ser:<br /><br /> Enviada para o cliente para que confie em qualquer servidor que apresente a mesma identificação digital ao ligar.<br /><br /> – Se o dispositivo ainda não incluir a identificação digital, pedirá ao utilizador para confiar no servidor VPN que estão a ligar e mostrar a identificação digital (o utilizador verifica-a manualmente e escolhe **confiança** para ligar).|VPN Móvel do Ponto de Verificação|  
|**Enviar todo o tráfego de rede através da ligação VPN** |Se esta opção não estiver selecionada, pode especificar rotas adicionais para a ligação (para os tipos de ligação **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** e **L2TP** ), o que é conhecido como túnel dividido ou VPN.<br /><br /> Apenas as ligações à rede da empresa são enviadas através de um túnel VPN. Os túneis VPN não são utilizados ao ligar-se a recursos na Internet. |Todas|  
|**Sufixo DNS específico da ligação** |O sufixo do sistema de nomes de domínio (DNS) específico da ligação para a ligação.|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**Ignorar a VPN quando ligado à rede Wi-Fi da empresa**  |A ligação VPN não será utilizada quando o dispositivo estiver ligado à rede Wi-Fi da empresa.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN Móvel do Ponto de Verificação<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatic<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**Ignorar a VPN quando ligado à rede Wi-Fi doméstica**  |A ligação VPN não será utilizada quando o dispositivo está ligado à rede Wi-Fi doméstica.|Todas|  
|**VPN Por Aplicação (iOS 7 e posterior, Mac OS X 10.9 e posterior)** |Associe esta ligação VPN a uma aplicação do iOS, para que a ligação seja aberta quando a aplicação é executada. Pode associar o perfil VPN a uma aplicação ao implementá-lo.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN Móvel do Ponto de Verificação|  
|**XML Personalizado (opcional)** |Especifique comandos XML personalizados que configuram a ligação VPN.<br /><br /> Exemplos:<br /><br /> Para **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> Para **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Para **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\> <br /> &nbsp; &nbsp; &lt;compressão\>falso&lt;/Compression\> <br /> &nbsp; &nbsp; &lt;debugLogging\>verdadeira&lt;/debugLogging\> <br /> &nbsp; &nbsp; &lt;/packetcapture\>falso&lt;/packetCapture\> <br /> &lt;/MobileConnect\>**<br /><br /> Para **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Consulte a documentação de cada fabricante relativa à VPN para mais informações sobre como escrever comandos XML personalizados.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - VPN Móvel do Ponto de Verificação|  

> [!NOTE]  
>  Para obter informações específicas para a criação de perfis VPN para dispositivos móveis, consulte [criar perfis de VPN](../../mdm/deploy-use/create-vpn-profiles.md)  

Conclua o assistente. O novo perfil VPN é apresentado no nó **Perfis VPN** da área de trabalho **Ativos e Compatibilidade** .

### <a name="next-steps"></a>Passos seguintes

- Para conexões de VPN de terceiros, distribua a aplicação VPN antes de implementar o perfil VPN. Se não implementar a aplicação, serão pedido aos utilizadores para fazê-lo quando o utilizador tentar estabelecer ligação à VPN. Para saber como implementar aplicações, veja [implementar aplicações com o System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Implemente o perfil da VPN, conforme descrito em [como implementar perfis no System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
