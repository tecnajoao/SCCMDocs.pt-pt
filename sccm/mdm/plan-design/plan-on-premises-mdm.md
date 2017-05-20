---
title: Planear no local MDM | Documentos do Microsoft
description: "Planear a gestão de dispositivos móveis no local gerir dispositivos móveis no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 507bad02c6e028f09a8b0c8a566ac55f7c3942a5
ms.openlocfilehash: 544c3bea0c7df96887ee1717f061c39c64b82d01
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planear a Gestão de Dispositivos Móveis no Local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Considere os requisitos seguintes antes de preparação da infraestrutura do Configuration Manager para processar no\-local gestão de dispositivos móveis.

##  <a name="bkmk_devices"></a>Dispositivos suportados  
 No local gestão de dispositivos móveis permite-lhe gerir dispositivos móveis ao utilizar as capacidades de gestão contempla os sistemas operativos de dispositivos.  A capacidade de gestão baseia-se na norma de Gestão de Dispositivos da Open Mobile Alliance (OMA) e muitas plataformas de dispositivos utilizam esta norma para permitir a gestão dos dispositivos.  Chamamos estas **dispositivos modernos** (na documentação do e a interface de utilizador de consola do Configuration Manager) para distingui-las a partir de outros dispositivos que necessitam de cliente do Configuration Manager para geri-los.  

 > [!NOTE]  
>  O ramo atual do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para os dispositivos que executem os seguintes sistemas operativos:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(partir 1602 de versão do Configuration Manager\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a>Utilização de subscrição do Microsoft Intune  
 Para começar a utilizar no\-local gestão de dispositivos móveis, terá de uma subscrição do Microsoft Intune. A subscrição só é necessária para controlar o licenciamento dos dispositivos e não é utilizada para gerir ou armazenar informações de gestão dos dispositivos. Toda a gestão é processada da empresa da sua organização utilizar a infraestrutura do Configuration Manager no local.  

 > [!NOTE]  
 > A partir na versão 1610, o Configuration Manager suporta a gerir dispositivos móveis com o Microsoft Intune e na infraestrutura no local do Configuration Manager ao mesmo tempo.   

 Se o seu site tiver dispositivos com ligação à internet, o serviço Intune pode ser utilizado para notificar os dispositivos para verificar o ponto de gestão de dispositivos para actualizações de política. Esta utilização do Intune é estritamente para notificação apenas de dispositivos de acesso à internet. Dispositivos sem ligações à internet (e não pode ser contactado pelo Intune) baseiam-se no intervalo de consulta configurado para verificar com funções de sistema de sites para funções de gestão.  

> [!TIP]  
>  Recomendamos que configure o Intune antes de configurar as funções do sistema de sites necessários para minimizar o tempo necessário para as funções do sistema de site para se tornarem funcional.  

 Para obter informações sobre como configurar a subscrição do Intune, consulte o artigo [configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a>Funções de sistema de sites necessários  
 No\-local gestão de dispositivos móveis requer, pelo menos, um de cada uma das seguintes funções do sistema de sites:  

-   **Ponto proxy de registo** para suportar pedidos de inscrição.  

-   **Ponto de inscrição** para suportar a inscrição de dispositivos.  

-   **Ponto de gestão de dispositivos** para entrega de políticas. Esta função do sistema de sites é uma variação da função de ponto de gestão que foi configurada para permitir a gestão de dispositivos móveis.  

-   **Ponto de distribuição** para a entrega de conteúdo.  

-   **Ponto de ligação de serviço** para ligar para o Intune para notificar dispositivos fora da firewall.  

 Estas funções de sistema de sites podem ser instaladas no servidor do sistema de sites único ou podem ser executadas separadamente em servidores diferentes, consoante as necessidades da sua organização. Cada servidor do sistema de site utilizado para no\-local gestão de dispositivos móveis tem de ser configurado como um ponto final de HTTPS para comunicação com os dispositivos fidedignos. Para obter mais informações, veja [Comunicações fidedignas necessárias](#bkmk_trustedComs).  

 Para obter mais informações sobre o posicionamento de funções do sistema de sites, veja [Planear os servidores do sistema de sites e as funções do sistema de sites para o System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Para obter mais informações sobre como adicionar as funções necessárias do sistema de site, veja [Instalar funções do sistema de sites para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a>Comunicações fidedignas necessárias  
 No\-local funções de sistema de sites para estar ativada nas comunicações HTTPS necessita de gestão de dispositivos móveis. Consoante as suas necessidades, pode utilizar a autoridade de certificação (AC) da sua empresa para estabelecer as ligações fidedignas entre servidores e dispositivos ou pode utilizar uma AC disponível ao público para ser a autoridade fidedigna.  De qualquer forma, irá precisar que um certificado do servidor Web seja configurado com o IIS nos servidores do sistema de sites que alojam as funções do sistema de sites necessárias e irá precisar do certificado de raiz dessa AC instalado nos dispositivos que necessitam de ligar a esses servidores.  

 Se utilizar a AC da sua empresa para estabelecer comunicações fidedignas, terá de realizar as seguintes tarefas:  

-   Criar e emitir o modelo do certificado do servidor Web na AC.  

-   Solicitar um certificado de servidor Web para cada servidor do sistema de sites que aloja uma função do sistema de sites necessária.  

-   Configurar o IIS no servidor do sistema de sites para utilizar o certificado do servidor Web solicitado.  

 No caso de dispositivos associados ao domínio do Active Directory da empresa, o certificado de raiz da AC empresarial já se encontra disponível no dispositivo para ligações fidedignas. Isto significa que os dispositivos associados a um domínio (como computadores de secretária) serão considerados automaticamente fidedignos para ligações HTTPS com os servidores do sistema de sites. No entanto, os dispositivos não associados a um domínio (normalmente, dispositivos móveis) não terão o certificado de raiz necessário instalado. Os dispositivos serão requerem o certificado de raiz para ser instalado manualmente nos mesmos para comunicar com suporte nos servidores de sistema de sites com êxito\-local gestão de dispositivos móveis.  

 Tem de exportar o certificado de raiz da AC emissora para utilização pelos dispositivos individuais. Para obter o ficheiro de certificado de raiz, pode exportá-lo utilizando a AC ou um método mais simples que consiste em utilizar o certificado do servidor Web emitido pela AC para extrair a raiz e criar um ficheiro de certificado de raiz.   Em seguida, o certificado de raiz tem de ser entregue no dispositivo.  Alguns exemplos de métodos de entrega incluem  

-   Sistema de ficheiros  

-   Anexo de e-mail  

-   Cartão de memória  

-   Dispositivo tethered  

-   Armazenamento na nuvem (por exemplo, o OneDrive)  

-   Ligação de comunicação de proximidade (NFC)  

-   Leitor de código de barras  

-   Pacote de aprovisionamento OOBE (out of box experience)  

 Para obter mais informações, veja [Configurar certificados para comunicações fidedignas para a Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a>Considerações de inscrição  
 Para ativar a inscrição de dispositivos no\-local gestão de dispositivos móveis, os utilizadores têm de possuir permissão para inscrever e os respetivos dispositivos devem ser capazes de ter fidedignidade comunicações com os servidores de sistema de sites que aloja as funções do sistema de sites necessários.  

 Conceder a permissão de inscrição do utilizador pode ser conseguida através de configurar um perfil de inscrição nas definições de cliente do Configuration Manager. Pode utilizar as predefinições de cliente para emitir o perfil de inscrição para todos os utilizadores detetados ou pode configurar o perfil de inscrição nas definições de cliente personalizadas e emitir as definições para uma ou mais coleções de utilizador.  

 Com a permissão de inscrição de utilizadores concedida, os utilizadores podem inscrever os respetivos dispositivos. Para ser inscrito, o dispositivo do utilizador tem de ter o certificado de raiz da autoridade de certificação (AC) que emitiu o certificado do servidor Web utilizado nos servidores do sistema de sites que alojam as funções do sistema de sites necessárias.  

 Como alternativa para a inscrição iniciada pelo utilizador, pode configurar um pacote de inscrição em volume que permite que o dispositivo seja inscrito sem a intervenção do utilizador. Este pacote pode ser fornecido ao dispositivo antes de ser inicialmente aprovisionado para utilização ou depois de o dispositivo passar pelo respetivo processo OOBE.  

 Para mais informações sobre como configurar e inscrever dispositivos, consulte  

-   [Configurar a inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Inscrever dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  

