---
title: Planear a MDM no local
titleSuffix: Configuration Manager
description: Planear a gestão de dispositivos móveis no local gerir dispositivos móveis no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 577672a6f816eaffc88c78d4baf3feab5b8989a1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132188"
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planear a Gestão de Dispositivos Móveis no Local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Considere os seguintes requisitos antes de preparar a infraestrutura do Configuration Manager para processar\-no local a gestão de dispositivos móveis.

##  <a name="bkmk_devices"></a> Dispositivos suportados  
 No local gestão de dispositivos móveis permite-lhe gerir dispositivos móveis ao utilizar as capacidades de gestão incorporadas nos sistemas operativos dos dispositivos.  A capacidade de gestão baseia-se na norma de Gestão de Dispositivos da Open Mobile Alliance (OMA) e muitas plataformas de dispositivos utilizam esta norma para permitir a gestão dos dispositivos.  Chamamos a estes **dispositivos modernos** (na documentação e a interface de utilizador de consola do Configuration Manager) para distingui-los de outros dispositivos que necessitam de cliente do Configuration Manager para geri-los.  

 > [!NOTE]  
>  O current branch do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos com os seguintes sistemas operativos:  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \(a partir do Configuration Manager versão 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Utilização da subscrição do Microsoft Intune  
 Para começar a utilizar no\-no local a gestão de dispositivos móveis, terá de uma subscrição do Microsoft Intune. A subscrição só é necessária para controlar o licenciamento dos dispositivos e não é utilizada para gerir ou armazenar informações de gestão dos dispositivos. Gestão de todos os é feita pela sua organização com a infraestrutura do Configuration Manager no local.  

 > [!NOTE]  
 > Partir da versão 1610, o Configuration Manager suporta a gestão de dispositivos móvel com o Microsoft Intune e de infraestrutura do Configuration Manager no local ao mesmo tempo.   

 Se o seu site tiver dispositivos com ligação à internet, o serviço do Intune pode ser utilizado para notificar dispositivos para verificar a gestão de dispositivos de ponto de atualizações à política de. Esta utilização do Intune é estritamente a notificação apenas de dispositivos de acesso à internet. Dispositivos sem ligação à internet (e não puder ser contatado pelo Intune) dependem do intervalo de consulta configurado para dar entrada com funções de sistema de sites para funções de gestão.  

> [!TIP]  
>  Recomendamos que configure o Intune antes de configurar as funções do sistema de sites necessárias para minimizar o tempo necessário para as funções de sistema de sites fiquem funcionais.  

 Para obter informações sobre como configurar a subscrição do Intune, consulte [configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Funções do sistema de sites necessárias  
 No\-locais a gestão de dispositivos móveis requer pelo menos um de cada uma das seguintes funções do sistema de sites:  

- **Ponto proxy de registo** para suportar pedidos de inscrição.  

- **Ponto de inscrição** para suportar a inscrição de dispositivos.  

- **Ponto de gestão de dispositivos** para entrega de políticas. Esta função do sistema de sites é uma variação da função de ponto de gestão que foi configurada para permitir a gestão de dispositivos móveis.  

- **Ponto de distribuição** para a entrega de conteúdo.  

- **Ponto de ligação de serviço** para ligar ao Intune para notificar dispositivos fora da firewall.  

  Estas funções de sistema de sites podem ser instaladas no servidor do sistema de sites único ou podem ser executadas separadamente em servidores diferentes, consoante as necessidades da sua organização. Cada servidor de sistema de sites utilizado para no\-locais gestão de dispositivos móveis tem de ser configurados como um ponto final HTTPS para comunicação com dispositivos fidedignos. Para obter mais informações, veja [Comunicações fidedignas necessárias](#bkmk_trustedComs).  

  Para obter mais informações sobre o posicionamento de funções do sistema de sites, veja [Planear os servidores do sistema de sites e as funções do sistema de sites para o System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

  Para obter mais informações sobre como adicionar as funções necessárias do sistema de site, veja [Instalar funções do sistema de sites para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Comunicações fidedignas necessárias  
 No\-locais funções de sistema de sites para ser ativada para comunicações HTTPS requer a gestão de dispositivos móveis. Consoante as suas necessidades, pode utilizar a autoridade de certificação (AC) da sua empresa para estabelecer as ligações fidedignas entre servidores e dispositivos ou pode utilizar uma AC disponível ao público para ser a autoridade fidedigna.  De qualquer forma, irá precisar que um certificado do servidor Web seja configurado com o IIS nos servidores do sistema de sites que alojam as funções do sistema de sites necessárias e irá precisar do certificado de raiz dessa AC instalado nos dispositivos que necessitam de ligar a esses servidores.  

 Se utilizar a AC da sua empresa para estabelecer comunicações fidedignas, terá de realizar as seguintes tarefas:  

- Criar e emitir o modelo do certificado do servidor Web na AC.  

- Solicitar um certificado de servidor Web para cada servidor do sistema de sites que aloja uma função do sistema de sites necessária.  

- Configurar o IIS no servidor do sistema de sites para utilizar o certificado do servidor Web solicitado.  

  No caso de dispositivos associados ao domínio do Active Directory da empresa, o certificado de raiz da AC empresarial já se encontra disponível no dispositivo para ligações fidedignas. Isto significa que os dispositivos associados a um domínio (como computadores de secretária) serão considerados automaticamente fidedignos para ligações HTTPS com os servidores do sistema de sites. No entanto, os dispositivos não associados a um domínio (normalmente, dispositivos móveis) não terão o certificado de raiz necessário instalado. Os dispositivos irão necessitar que o certificado de raiz seja instalado manualmente nos mesmos para comunicar com êxito com servidores de sistema de sites que suportam no\-no local a gestão de dispositivos móveis.  

  Tem de exportar o certificado de raiz da AC emissora para utilização pelos dispositivos individuais. Para obter o ficheiro de certificado de raiz, pode exportá-lo utilizando a AC ou um método mais simples que consiste em utilizar o certificado do servidor Web emitido pela AC para extrair a raiz e criar um ficheiro de certificado de raiz.   Em seguida, o certificado de raiz tem de ser entregue no dispositivo.  Alguns exemplos de métodos de entrega incluem  

- Sistema de ficheiros  

- Anexo de e-mail  

- Cartão de memória  

- Dispositivo tethered  

- Armazenamento na nuvem (por exemplo, o OneDrive)  

- Ligação de comunicação de proximidade (NFC)  

- Leitor de código de barras  

- Pacote de aprovisionamento OOBE (out of box experience)  

  Para obter mais informações, veja [Configurar certificados para comunicações fidedignas para a Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="bkmk_enrollment"></a> Considerações sobre inscrição  
 Para ativar a inscrição de dispositivos para no\-local gestão de dispositivos móveis, os utilizadores têm de ser concedidos permissão para inscrever e seus dispositivos tem de ser capazes de ter comunicações fidedignas com os servidores de sistema de sites que alojam as funções de sistema de sites necessárias.  

 Conceder permissão de inscrição de utilizador pode ser feito ao configurar um perfil de inscrição nas definições de cliente do Configuration Manager. Pode utilizar as predefinições de cliente para emitir o perfil de inscrição para todos os utilizadores detetados ou pode configurar o perfil de inscrição nas definições de cliente personalizadas e emitir as definições para uma ou mais coleções de utilizador.  

 Com a permissão de inscrição de utilizadores concedida, os utilizadores podem inscrever os respetivos dispositivos. Para ser inscrito, o dispositivo do utilizador tem de ter o certificado de raiz da autoridade de certificação (AC) que emitiu o certificado do servidor Web utilizado nos servidores do sistema de sites que alojam as funções do sistema de sites necessárias.  

 Como alternativa para a inscrição iniciada pelo utilizador, pode configurar um pacote de inscrição em volume que permite que o dispositivo seja inscrito sem a intervenção do utilizador. Este pacote pode ser fornecido ao dispositivo antes de ser inicialmente aprovisionado para utilização ou depois de o dispositivo passar pelo respetivo processo OOBE.  

 Para mais informações sobre como configurar e inscrever dispositivos, consulte  

-   [Configurar a inscrição de dispositivos para gestão de dispositivos móveis no local no System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Inscrever dispositivos para Gestão de Dispositivos Móveis no Local do System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
