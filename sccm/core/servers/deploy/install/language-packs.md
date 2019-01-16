---
title: Pacotes de idiomas
titleSuffix: Configuration Manager
description: Saiba mais sobre o suporte de idioma disponível no Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f6b10706638a476242051757145f725b262a7fc
ms.sourcegitcommit: 2687489aa409a050dcacd67f17b3dad3ab7f1804
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54316444"
---
# <a name="language-packs-in-configuration-manager"></a>Pacotes de idiomas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece detalhes técnicos sobre o suporte de idiomas no Configuration Manager. Servidores de site do Configuration Manager e os clientes são considerados idioma neutro. Adicionar suporte para idiomas de apresentação através da instalação **pacotes de idiomas de servidor** ou **pacotes de idiomas de cliente** num site de administração central e em sites primários. Selecione os idiomas de servidor e cliente para suportar num site a partir de ficheiros do pacote de idiomas disponíveis durante o processo de instalação do site.
 
Instale vários idiomas em cada site. Apenas terá de instalar os idiomas que utiliza.  

- Cada site suporta vários idiomas para consolas do Configuration Manager.  

- Adicione suporte para apenas os idiomas de cliente que pretende suportar instalando pacotes de idiomas de cliente individuais em cada site.  

Quando instala suporte para um idioma que corresponde aos seguintes componentes:  

- O idioma de apresentação de um computador: Consola do Configuration Manager e a interface de utilizador do cliente que executa nesse computador apresentam informações nesse idioma.  

- A preferência de idioma que está a ser utilizada pelo browser de um computador: Ligações a informações baseadas na web, incluindo o catálogo de aplicações ou o SQL Server Reporting Services, apresentadas nesse idioma.  


Quando executar a configuração do Configuration Manager, transfere ficheiros do pacote de idioma como parte dos pré-requisitos e os ficheiros redistribuíveis. Também pode utilizar o [configurar o dispositivo de transferência da](setup-downloader.md) para transferir estes ficheiros antes de executar a configuração.   



## <a name="server-languages"></a>Idiomas do servidor  

Utilize a tabela seguinte para mapear um ID de região para um idioma que pretende suportar em servidores. Para obter mais informações sobre IDs de região, consulte [IDs de região atribuídos pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Idioma do servidor|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENU|  
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



## <a name="client-languages"></a>Idiomas de cliente  

Utilize a tabela seguinte para mapear um ID de região para um idioma que pretende suportar em computadores cliente. Para obter mais informações sobre IDs de região, consulte [IDs de região atribuídos pela Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Idioma do cliente|ID de região (LCID)|Código de três letras|  
|---------------------|------------------------|-----------------------|  
|Inglês (predefinição)|0409|ENG|  
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
Quando adiciona suporte para idiomas do dispositivo móvel, todos os idiomas de cliente de dispositivos móveis suportadas estão incluídos. Não é possível selecionar pacotes de idiomas individuais para suporte de dispositivos móveis.  



## <a name="identify-installed-language-packs"></a>Identificar pacotes de idiomas instalados  
Para identificar os pacotes de idiomas instalados num computador que executa o cliente do Configuration Manager, procure o ID de região (LCID) dos pacotes de idiomas instalados no registo do computador. Esta informação estiver disponível no seguinte caminho de registo:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personalize o inventário de hardware para recolher estas informações. Em seguida, crie um relatório personalizado para ver os detalhes do idioma. Para obter mais informações sobre a recolha de inventário de hardware personalizado, consulte [como configurar inventário de hardware](/sccm/core/clients/manage/inventory/configure-hardware-inventory). Para obter mais informações sobre a criação de relatórios, consulte [relatórios do Configuration Manager/gerir](/sccm/core/servers/manage/operations-and-maintenance-for-reporting#BKMK_ManageReports).  
