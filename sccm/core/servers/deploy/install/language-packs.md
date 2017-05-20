---
title: Pacotes de idiomas | Documentos do Microsoft
description: "Saiba mais sobre o suporte de idioma disponível no System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: e7075eb675353be130fdcc867d9e4dd1009dab35
ms.openlocfilehash: 47da3c531289ddf13d357bde8bbda85d79ed2803
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="language-packs-in-system-center-configuration-manager"></a>Pacotes de idiomas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece detalhes técnicos sobre o suporte de idiomas no System Center Configuration Manager.  

## <a name="BKMK_SupLanguagePacks"></a>Idiomas de sistema operativo suportado  
 É possível instalar suporte para os idiomas de apresentação nas tabelas seguintes instalando **pacotes de idiomas de servidor** ou **pacotes de idiomas de cliente** num site de administração central e em sites primários. Selecione os idiomas de servidor e cliente para suportar um site a partir dos ficheiros do pacote de idioma disponível durante o processo de instalação do site.

 Ficheiros do pacote de idioma são transferidos quando executa a configuração como parte dos pré-requisitos e a transferência do ficheiro redistributable. Também pode utilizar [dispositivo de transferência da configuração](setup-downloader.md) transferir estes ficheiros antes de executar a configuração.   

 Utilize a tabela seguinte para mapear um ID de região para um idioma que pretende suportar em servidores ou computadores cliente. Para obter mais informações sobre IDs de região, consulte o artigo [IDs de região atribuídos pela Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609).  

### <a name="server-languages"></a>Idiomas do servidor  

|Idioma do servidor|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENU|  
|Chinês (Tradicional, R.A.E. Hong Kong)|0c04|ZHH|  
|Chinês (Simplificado)|0804|CHS|  
|Chinês (Tradicional, Taiwan)|0404|CHT|  
|Checo|0405|CSY|  
|Neerlandês (Países Baixos)|0413|NLD|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Húngaro|040e|HUN|  
|Italiano (Itália)|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Polaco|0415|PLK|  
|Português (Brasil)|0416|PTB|  
|Português (Portugal)|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol (Espanha)|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="client-languages"></a>Idiomas de cliente  

|Idioma do cliente|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENG|  
|Chinês (Tradicional, R.A.E. Hong Kong)|0c04|ZHH|  
|Chinês (Simplificado)|0804|CHS|  
|Chinês (Tradicional, Taiwan)|0404|CHT|  
|Checo|0405|CSY|  
|Dinamarquês|0406|DAN|  
|Neerlandês (Países Baixos)|0413|NLD|  
|Finlandês|040b|FIN|  
|Francês|040c|FRA|  
|Alemão|0407|DEU|  
|Grego|0408|ELL|  
|Húngaro|040e|HUN|  
|Italiano (Itália)|0410|ITA|  
|Japonês|0411|JPN|  
|Coreano|0412|KOR|  
|Norueguês|0414|NOR|  
|Polaco|0415|PLK|  
|Português (Brasil)|0416|PTB|  
|Português (Portugal)|0816|PTG|  
|Russo|0419|RUS|  
|Espanhol (Espanha)|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Idiomas de cliente do dispositivo móvel  
 Quando adiciona suporte para idiomas do dispositivo móvel, todos os idiomas de cliente de dispositivo móvel suportados estão incluídos. É possível selecionar pacotes de idiomas individuais para suporte de dispositivos móveis.  

### <a name="identify-installed-language-packs"></a>Identificar pacotes de idiomas instalados  
Para identificar os pacotes de idiomas que estão instalados num computador que executa o cliente do Configuration Manager, procure o ID de região (LCID) dos pacotes de idiomas instalados no registo do computador. Estas informações ficam disponíveis em:

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Pode utilizar o inventário de hardware para recolher estas informações e, em seguida, criar um relatório personalizado para ver os detalhes do idioma. Para obter informações sobre a recolha do inventário de hardware personalizado, consulte o artigo [como configurar inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). Para obter informações sobre a criação de relatórios, consulte o [relatórios do Configuration Manager gerir](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) secção a [operações e manutenção de relatórios no System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md) tópico.  
