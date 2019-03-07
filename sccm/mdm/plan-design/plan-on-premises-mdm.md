---
title: Planear a MDM no local
titleSuffix: Configuration Manager
description: Planear a gestão de dispositivos móveis no local gerir dispositivos móveis no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558087"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planear a MDM no local no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Gestão de dispositivos móveis no local (MDM) permite-lhe gerir dispositivos móveis utilizando as capacidades de gestão incorporadas no SO do dispositivo. A capacidade de gestão baseia-se na norma de Gestão de Dispositivos da Open Mobile Alliance (OMA) e muitas plataformas de dispositivos utilizam esta norma para permitir a gestão dos dispositivos. Estes dispositivos são chamados *dispositivos modernos* na documentação e a consola do Configuration Manager. Esse termo distingue-los de outros dispositivos que necessitam de cliente do Configuration Manager para geri-los.  

Considere os seguintes requisitos antes de preparar a infraestrutura do Configuration Manager para lidar com a MDM no local.



## <a name="bkmk_devices"></a> Dispositivos suportados  

O current branch do Configuration Manager suporta a inscrição na gestão de dispositivos móveis no local para dispositivos com os seguintes sistemas operativos:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a> A subscrição do Microsoft Intune  

Para começar a utilizar o MDM no local, terá de uma subscrição do Microsoft Intune. A subscrição é necessário apenas para controlar o licenciamento dos dispositivos e não é utilizada para gerir ou armazenar informações de gestão para os dispositivos. Todos os dados de gestão são armazenados na sua organização com a infraestrutura do Configuration Manager no local.  

> [!Note]  
> A partir da versão 1810, uma ligação do Intune já não é necessária para novas implementações de MDM no local.<!--3607730, fka 1359124--> Sua organização ainda requer licenças do Intune para utilizar esta funcionalidade. Atualmente não é possível remover a ligação do Intune a partir de implementações de MDM no local existentes. Para obter mais informações, consulte a [mensagem de blogue de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Se o seu site tiver dispositivos com ligação à internet, o serviço do Intune pode ser utilizado para notificar dispositivos para verificar a gestão de dispositivos de ponto de atualizações à política de. Este comportamento utiliza o Intune estritamente para notificação de dispositivos de acesso à internet. Dispositivos sem ligações à internet e que não pode ser contatado pelo Intune dependem de intervalo de consulta configurado para dar entrada com funções de sistema de sites para funções de gestão.  

> [!TIP]  
> Antes de configurar as funções do sistema de sites necessárias, configure a subscrição do Intune. Esta ação minimiza o tempo necessário para as funções fiquem funcionais.  

Para obter informações sobre como configurar a subscrição do Intune, consulte [configurar uma subscrição do Microsoft Intune para MDM no local](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Site system roles  

No local MDM requer pelo menos um de cada uma das seguintes funções do sistema de sites:  

- **Ponto proxy de registo** para suportar pedidos de inscrição.  

- **Ponto de inscrição** para suportar a inscrição de dispositivos.  

- **Ponto de gestão de dispositivos** para entrega de políticas. Esta função do sistema de sites é uma variação da função de ponto de gestão que foi configurada para permitir a gestão de dispositivos móveis.  

- **Ponto de distribuição** para a entrega de conteúdo.  

- **Ponto de ligação de serviço** para ligar ao Intune para notificar dispositivos fora da firewall.  

Estas funções de sistema de sites podem ser instaladas no servidor do sistema de site único ou podem ser executadas separadamente em servidores diferentes, consoante as necessidades da sua organização. Cada servidor de sistema de sites utilizado para MDM no local tem de ser configurado como um ponto final HTTPS para comunicação com dispositivos fidedignos. Para obter mais informações, veja [Comunicações fidedignas necessárias](#bkmk_trustedComs).  

Para obter mais informações sobre o planeamento de funções do sistema de sites, consulte [planear servidores de sistema de sites e funções para o Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Para obter mais informações sobre como adicionar as funções do sistema de sites necessárias, consulte [instalar funções do sistema de sites para MDM no local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Comunicações fidedignas  

MDM no local requer que as funções de sistema de sites para ser ativada para comunicações HTTPS. Consoante as suas necessidades, pode utilizar a autoridade de certificação da sua empresa (AC) para estabelecer as ligações fidedignas entre servidores e dispositivos. Também pode utilizar uma AC publicamente disponível para ser a autoridade fidedigna. De qualquer forma, terá de um certificado de servidor web a serem configurados em IIS nos servidores de sistema de sites que alojam as funções de sistema de sites necessárias. Também tem do certificado de raiz dessa AC instalado nos dispositivos que precisam de ligar a esses servidores.  

Se utilizar a AC da sua empresa para estabelecer comunicações fidedignas, efetue as seguintes tarefas:  

- Criar e emitir o modelo do certificado do servidor Web na AC.  

- Solicitar um certificado de servidor Web para cada servidor do sistema de sites que aloja uma função do sistema de sites necessária.  

- Configurar o IIS no servidor do sistema de sites para utilizar o certificado do servidor Web solicitado.  

No caso de dispositivos associados ao domínio do Active Directory da empresa, o certificado de raiz da AC empresarial já se encontra disponível no dispositivo para ligações fidedignas. Este comportamento significa que os dispositivos associados a domínios são automaticamente fidedignos para ligações de HTTPS com os servidores de sistema de sites. No entanto, dispositivos não associados ao domínio não recebem automaticamente o certificado de raiz necessário instalado. Para comunicar com êxito com servidores de sistema de sites que suportam a MDM no local, dispositivos não associados ao domínio, como dispositivos móveis tem de instalar manualmente o certificado de raiz nos mesmos.  

Exporte o certificado de raiz da AC emissora para utilização pelos dispositivos individuais. Para obter o ficheiro de certificado de raiz, pode exportá-lo utilizando a AC. Outro método consiste em utilizar o certificado de servidor web emitido pela AC para extrair a raiz e crie um ficheiro de certificado de raiz. Em seguida, o certificado de raiz tem de ser fornecido ao dispositivo. Alguns métodos de entrega de exemplo incluem:

- Sistema de ficheiros  

- Anexo de e-mail  

- Cartão de memória  

- Dispositivo tethered  

- Armazenamento na nuvem (por exemplo, o OneDrive)  

- Ligação de comunicação de proximidade (NFC)  

- Leitor de código de barras  

- Pacote de aprovisionamento OOBE (out of box experience)  

Para obter mais informações, consulte [configurar certificados para comunicações fidedignas no MDM no local](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Inscrição de dispositivos

Para ativar a inscrição de dispositivos para MDM no local,
- Devem ser concedido aos utilizadores permissão para inscrever 
- Dispositivos tem de ser configurados para comunicações fidedignas com os servidores de sistema de sites que alojam as funções necessárias  

Conceda aos utilizadores permissão para inscrever dispositivos por configurar um perfil de inscrição nas definições de cliente do Configuration Manager. Pode utilizar as predefinições de cliente para emitir o perfil de inscrição para todos os utilizadores detetados. Também pode configurar o perfil de inscrição nas definições de cliente personalizadas e emitir as definições para um ou mais coleções de utilizadores.  

Assim que os utilizadores que terão permissão, pode inscrever os seus próprios dispositivos. Para ser inscrito, o dispositivo do utilizador tem de ter o certificado de raiz da autoridade de certificação (AC) que emitiu o certificado de servidor web utilizado nos servidores de sistema de sites que alojam as funções necessárias.  

Como alternativa à inscrição iniciada pelo utilizador, pode configurar um pacote de inscrição em massa. Este pacote permite que o dispositivo seja inscrito sem intervenção do utilizador. Pode ser fornecido ao dispositivo antes de que está aprovisionado para utilização ou depois do dispositivo passar pelo respetivo processo OOBE.  

Para obter mais informações sobre como configurar e inscrever dispositivos, consulte os artigos seguintes: 

- [Configurar a inscrição de dispositivos para MDM no local](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Inscrever dispositivos para MDM no local](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

