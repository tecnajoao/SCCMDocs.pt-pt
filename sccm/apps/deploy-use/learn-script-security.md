---
title: Saiba mais sobre a segurança de script do PowerShell
titleSuffix: Configuraton Manager
description: Recursos para ajudar a saber mais sobre a segurança de script do PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7799ac9737ac3a6a73d2d7241dd8b56325d4e340
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343716"
---
# <a name="learn-more-about-powershell-script-security"></a>Saiba mais sobre a segurança de script do PowerShell

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Responsabilidade do administrador para validar proposto PowerShell e o PowerShell utilização de parâmetros no respetivo ambiente. Seguem-se alguns recursos úteis para ajudar a informe os administradores sobre energia do PowerShell e analisa de risco potencial. Isto é ajudar a mitigar a potencial analisa de risco e permitir que os scripts seguros para ser utilizado.

## <a name="powershell-script-security"></a>Segurança de Script do PowerShell
Incorporado nos Scripts de executar é uma funcionalidade visualmente rever e aprovar scripts que são pedidos a ser executado no ambiente. Os administradores devem ter conhecimento de scripts do PowerShell podem ter ocultado script: scripts maliciosos e difíceis de detetar com visual inspeção durante o processo de aprovação de script. Como melhor prática, utilizando ferramentas determinadas inspeção, no adicionais para rever visualmente scripts do PowerShell, irá ajudar a detetar problemas de scripts suspeita. Estas ferramentas sempre não é possível determinar a intenção do autor do PowerShell para poder colocar atenção para um script suspeita. No entanto, as ferramentas requerem o administrador para avaliar se é sintaxe de script malicioso ou intencional.

## <a name="recommendations"></a>Recomendações
- Familiarize-se com o PowerShell melhores práticas de segurança utilizando as ligações de vários referenciadas abaixo.
- **Assinar os scripts**: Outro método para manter os scripts seguro é ter os mesmos possam vetted e, em seguida, com sessão iniciada, antes de importá-los para utilização.
- Não armazenar segredos (tal como as palavras-passe) em scripts do PowerShell e saber mais sobre como lidar com segredos.


## <a name="general-information-about-powershell-security-best-practices"></a>Informações gerais sobre práticas recomendadas de segurança de PowerShell

Esta coleção de ligações foi escolhida para dar um ponto de partida de administradores do Configuration Manager para aprender sobre práticas recomendadas de segurança de script do PowerShell.  

[Introdução ao práticas recomendadas de segurança de PowerShell](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell segurança melhores práticas PowerPoint](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defending contra PowerShell ataques, blogue da equipa do PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Twitter defending contra ataques de PowerShell, de um Microsoft PowerShell e segurança advocate Nogueira Holmes](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Proteger contra Injeção de código malicioso](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Informações sobre a segurança da galeria do PowerShell](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[Equipa azul o PowerShell, descreve o bloco de Script profunda a iniciar sessão, protegido registo de eventos, a Interface de análise Antimalware, proteger os APIs de geração de código](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Para o Windows 10, é uma API para uma interface de análise Antimalware](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Segurança de parâmetros de PowerShell
Os parâmetros a transmitir é uma forma flexibilidade com os scripts e diferir decisões até que o tempo de execução. Abre-se também configurar outra superfície de risco. Melhores práticas para impedir a injeção de script ou parâmetros maliciosos são:

- Permitir apenas a utilização de parâmetros predefinidos.
- Utilize a funcionalidade de expressão regular para validar os parâmetros que são permitidos.
    - Exemplo: Se apenas são permitidos um determinado intervalo de valores, utilize uma expressão regular para verificar se apenas esses carateres ou valores que podem fazer cópias de segurança do intervalo.
    - A validar os parâmetros pode ajudar a impedir que os utilizadores a tentar utilizar determinados caracteres que podem ser caráter de escape correto, como as aspas. Tenha em atenção que podem existir vários tipos de aspas, por isso, utilizando expressões regulares para validar que carateres tiver decidido são permitidos, muitas vezes, é mais fácil ao tentar definir todas as entradas que não permitido.
- Tirar partido do módulo do PowerShell ["hunter injeção"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) na galeria do PowerShell.
    - Não existe pode ser falsos positivos, por isso, procure para intenção quando algo está assinalada como suspeita para determinar se é um problema real ou não. 
- Microsoft Visual Studio tem um analisador de Script, que pode ajudar a verificar a sintaxe do PowerShell.
- Este vídeo intitulado: "DEF CON 25 - Nogueira Holmes - obter $pwnd: Atacar luta puro Windows Server"proporcione uma descrição geral dos tipos de problemas que pode proteger contra (especialmente a secção 12:20 para 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recomendações de ambiente
Recomendações gerais para os administradores do PowerShell.
1. Implemente uma versão mais recente do PowerShell, como a versão 5 ou superior, incorporadas no Windows 10. Em alternativa, pode implementar o [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616), disponível para baixo e incluindo, Windows 7 e Windows Server 2008 R2. 
2. Ative e recolher registos de PowerShell, opcionalmente incluindo protegidos registo de eventos. Incorpore estes registos suas assinaturas, hunting e fluxos de trabalho de resposta a incidentes.
3. Implemente apenas suficiente administração em sistemas de elevado valor, eliminar ou reduzir acesso administrativo a esses sistemas.
4. Implemente políticas de controlo de proteção/aplicação de dispositivo para permitir que as tarefas administrativas previamente aprovadas a utilizar da capacidade total do idioma do PowerShell, ao limitar utilização interativa e não aprovada para um subconjunto limitado do idioma do PowerShell.
5. Implementar o Windows 10 para dar o seu fornecedor de antivírus acesso total a todo o conteúdo (incluindo o conteúdo gerado ou anular oculto no tempo de execução) processado pelo Windows Scripting anfitriões, incluindo o PowerShell.