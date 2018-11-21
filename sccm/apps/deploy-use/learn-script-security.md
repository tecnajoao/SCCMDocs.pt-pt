---
title: Saiba mais sobre a segurança de script do PowerShell
titleSuffix: Configuration Manager
description: Recursos para ajudar a saber mais sobre segurança de script do PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b5f7ac3125b099a764604b3338a92f3f45b10afe
ms.sourcegitcommit: 2cc635835709fb8d86cdb63ea34233b36c94d4d8
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/20/2018
ms.locfileid: "52258983"
---
# <a name="learn-more-about-powershell-script-security"></a>Saiba mais sobre a segurança de script do PowerShell

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

É responsabilidade do administrador para validar a proposta PowerShell e o PowerShell utilização de parâmetros em seus ambientes. Aqui estão alguns recursos úteis para ajudar a educar os administradores sobre o poder do PowerShell e as possíveis superfícies de risco. Trata-se para o ajudar a atenuar possíveis superfícies de risco e permitir que scripts seguros para ser utilizado.

## <a name="powershell-script-security"></a>Segurança de Script do PowerShell
Incorporado ao executar Scripts é uma funcionalidade para visualmente rever e aprovar os scripts que são solicitados a ser executado no ambiente. Os administradores devem estar cientes de scripts do PowerShell podem ter oculto script: script malicioso e difícil de detetar com inspeção visual durante o processo de aprovação de script. Como melhor prática, usando determinadas ferramentas de inspeção, em adicionais para revisão visualmente scripts do PowerShell, irá ajudar a detetar problemas de scripts suspeitos. Essas ferramentas sempre não é possível determinar a intenção do autor do PowerShell para que ele pode trazer a atenção para um script que se suspeita. No entanto, as ferramentas irão exigir que o administrador avaliar se é a sintaxe de script malicioso ou intencional.

## <a name="recommendations"></a>Recomendações
- Familiarize-se com o PowerShell melhores práticas de segurança utilizando as várias ligações referenciadas abaixo.
- **Assinar seus scripts**: Outro método para manter scripts seguro é fazendo com que eles examinados e, em seguida, iniciar, antes de importá-los para utilização.
- Não armazenar segredos (tal como palavras-passe) em scripts do PowerShell e saiba mais sobre como lidar com segredos.


## <a name="general-information-about-powershell-security-best-practices"></a>Informações gerais sobre práticas recomendadas de segurança de PowerShell

Esta coleção de ligações foi escolhida para dar um ponto de partida de administradores do Configuration Manager para aprender sobre práticas recomendadas de segurança de script do PowerShell.  

[Introdução às práticas recomendadas de segurança de PowerShell](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerPoint de práticas recomendada do PowerShell segurança](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Blog da equipe de defending contra PowerShell ataques, do PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Lee Holmes de desenvolvimento do twitter defending contra ataques de PowerShell, do Microsoft PowerShell e segurança](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Proteção contra Injeção de código mal-intencionado](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Informações sobre a segurança da galeria do PowerShell](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[Equipa azul do PowerShell, discute o bloco de Script profunda Registro em log, registo de eventos protegidos, a Interface de análise de Antimalware, a proteger APIs de geração de código](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Para Windows 10, é uma API para uma interface de análise de antimalware](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Segurança de parâmetros do PowerShell
Passando parâmetros é uma forma de ter a flexibilidade com os seus scripts e diferir decisões até o Runtime. Ele também abre outra superfície de risco. Melhores práticas para impedi parâmetros maliciosos ou injeção de script são:

- Permitir apenas a utilização de parâmetros predefinidos.
- Utilize a funcionalidade de expressão regular, para validar parâmetros que são permitidos.
    - Exemplo: Se apenas um determinado intervalo de valores são permitidos, use uma expressão regular para verificar de apenas esses caracteres ou os valores que podem constituem o intervalo.
    - A validar os parâmetros pode ajudar a impedir que os utilizadores a tentar utilizar determinados caracteres que podem ser ignorados, como aspas. Lembre-se de que pode haver vários tipos de aspas, assim, usando expressões regulares para validar quais caracteres tiver decidido são permitidos, muitas vezes, é mais fácil do que tentar definir todas as entradas que não é permitido.
- Tire partido do módulo do PowerShell ["hunter injeção"](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) na galeria do PowerShell.
    - Aqui pode ser falsos positivos, então procura intenção quando algo for sinalizada como suspeito para determinar se é um problema real ou não. 
- Microsoft Visual Studio tem um analisador de Script, que pode ajudar com a verificação de sintaxe do PowerShell.
- Este vídeo intitulado: "DEF CON 25 - Lee Holmes - obter $pwnd: Atacar os batalha puro Windows Server"fornece uma descrição geral dos tipos de problemas que pode proteger contra (especialmente a secção 12:20 a 17:50):     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recomendações de ambiente
Recomendações gerais para administradores do PowerShell.
1. Implemente uma versão mais recente do PowerShell, por exemplo, a versão 5 ou superior, incorporado no Windows 10. Em alternativa, pode implementar o [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616), disponível para baixo e incluindo o Windows 7 e Windows Server 2008 R2. 
2. Ativar e recolher registos de PowerShell, opcionalmente, incluindo o registo de eventos protegidos. Incorpore estes registos suas assinaturas, buscar e fluxos de trabalho de resposta a incidentes.
3. Implemente a administração apenas suficiente em sistemas de grande valor para eliminar ou reduza o acesso administrativo irrestrita para esses sistemas.
4. Implemente políticas de controlo de Guard/aplicações de dispositivo para permitir que as tarefas administrativas pré-aprovados utilizar a capacidade total da linguagem do PowerShell, embora limitar a utilização de análises interativa e não aprovada para um subconjunto limitado da linguagem do PowerShell.
5. Implementar o Windows 10 para dar o seu fornecedor de antivírus acesso total a todo o conteúdo (incluindo o conteúdo gerado ou anular oculto no tempo de execução) processado pelo Windows Scripting anfitriões incluindo o PowerShell.