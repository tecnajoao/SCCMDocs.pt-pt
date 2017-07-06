# Descrição Geral
## [O que é a MDM híbrida](understand/hybrid-mobile-device-management.md)
## [Escolher o Intune autónomo ou a MDM híbrida](understand/choose-between-standalone-intune-and-hybrid-mobile-device-management.md)
## [Novidades sobre a MDM híbrida](understand/whats-new-in-hybrid-mobile-device-management.md)

# [Planear e estruturar](plan-design/plan-hybrid-mobile-device-management.md)
## [Plataformas de dispositivos suportadas](plan-design/supported-device-platforms-for-hybrid.md)
## [Métodos de inscrição de dispositivos](plan-design/device-enrollment-methods.md)

# [Introdução](deploy-use/setup-hybrid-mdm.md)
## [Criar uma coleção de MDM](deploy-use/create-mdm-collection.md)
## [Confirmar os requisitos de nomes de domínio](deploy-use/confirm-dns.md)
## [Configurar a subscrição do Intune](deploy-use/configure-intune-subscription.md)
## [Adicionar termos e condições](deploy-use/terms-and-conditions.md)
## [Criar um ponto de ligação de serviço](deploy-use/create-service-connection-point.md)
## [Ativar a inscrição da plataforma](deploy-use/enable-platform-enrollment.md)
### [iOS e MAC](deploy-use/enroll-hybrid-ios-mac.md)
### [Windows](deploy-use/enroll-hybrid-windows.md)
### [Android](deploy-use/enroll-hybrid-android.md)
## [Configurar gestão adicional](deploy-use/set-up-additional-management.md)
## [Verificar a configuração da MDM](deploy-use/verify-mdm-configuration.md)

# Procedimento
## [Inscrever dispositivos pertencentes ao utilizador (BYOD)](deploy-use/enroll-user-owned-devices.md)
## [Inscrever dispositivos pertencentes à empresa](deploy-use/enroll-company-owned-devices.md)
### [Inscrição de dispositivos iOS no DEP](deploy-use/ios-device-enrollment-program-for-hybrid.md)
### [Inscrição no Apple Configurator](deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)
### [Gestor de inscrição de dispositivos](deploy-use/enroll-devices-with-device-enrollment-manager.md)
### [Pré-declarar o ID de hardware](deploy-use/predeclare-devices-with-hardware-id.md)
### [Gerir o bloqueio de ativação do iOS](deploy-use/manage-ios-activation-lock.md)
### [Afinidade dispositivo/utilizador](deploy-use/user-affinity-for-hybrid-managed-devices.md)

## [Extinguir/limpar, bloquear, repor dispositivos](deploy-use/wipe-lock-reset-devices.md)
## [Configurar o inventário de hardware](deploy-use/mobile-device-hardware-inventory-hybrid.md)
## [Configurar o inventário de software](deploy-use/software-inventory-mobile-devices.md)

## [Gerir as definições de conformidade](deploy-use/manage-compliance-settings.md)
### [Windows 8.1 e Windows 10](deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
### [Windows Phone](deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
### [iOS e Mac OS X](deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
### [Android e Samsung KNOX Standard](deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)
### [Android for Work](deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client.md)

## [Sincronizar dispositivos inscritos no Intune](deploy-use/sync-intune-device.md)

## [Gerir aplicações](deploy-use/management-tasks-applications.md)
### [Criar aplicações iOS](deploy-use/creating-ios-applications.md)
### [Políticas de configuração de aplicações iOS](deploy-use/configure-ios-apps-with-app-configuration-policies.md)
### [Aplicações iOS compradas em volume](deploy-use/manage-volume-purchased-ios-apps.md)
### [Criar aplicações Windows Phone](deploy-use/creating-windows-phone-applications.md)
### [Criar aplicações Android](deploy-use/creating-android-applications.md)
### [Políticas de gestão de aplicações móveis](deploy-use/protect-apps-using-mam-policies.md)
### [Políticas de browser gerido](deploy-use/manage-internet-access-using-managed-browser-policies.md)
### [Aplicações da Loja Windows para Empresas](deploy-use/windows-store-for-business.md)

## [Gerir uma subscrição do Intune](deploy-use/manage-intune-subscriptions.md)

## [Alterar sua autoridade MDM](deploy-use/change-mdm-authority.md)

## Gerir o acesso a recursos
### [Criar perfis Wi-Fi](deploy-use/create-wifi-profiles.md)
### [Criar perfis de certificado PFX](deploy-use/create-pfx-certificate-profiles.md)
### [Perfis VPN](deploy-use/create-vpn-profiles.md)
### [Criar perfis de e-mail](deploy-use/create-exchange-activesync-profiles.md)
### [Definições do Windows Hello para Empresas ](deploy-use/windows-hello-for-business-settings.md)

## [Gerir o acesso condicional](deploy-use/manage-access-to-services.md)
### [Políticas de conformidade do dispositivo](deploy-use/device-compliance-policies.md)
### [Criar uma política de conformidade do dispositivo](deploy-use/create-compliance-policy.md)
### [Gerir o acesso ao e-mail](deploy-use/manage-email-access.md)
### [Gerir o acesso ao SharePoint Online](deploy-use/manage-sharepoint-online-access.md)
### [Gerir o acesso ao Skype para Empresas Online](deploy-use/manage-skype-for-business-online-access.md)
### [Gerir o acesso ao Dynamics CRM Online](deploy-use/manage-dynamics-crm-online-access.md)
### [Gerir o acesso dos PCs aos serviços do O365](deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)

## [Gerir o acesso com base no risco do dispositivo](deploy-use/mobile-threat-defense.md)
### [Lookout no Configuration Manager](deploy-use/lookout-mobile-threat-defense-in-configuration-manager.md)
#### [Configurar a Defesa Contra Ameaças para Dispositivos Móveis do Lookout](deploy-use/set-up-your-subscription-with-lookout.md)
#### [Ativar o Lookout no Intune](deploy-use/enable-lookout-connection-in-intune.md)
#### [Implementar a aplicação Lookout for Work](deploy-use/configure-and-deploy-lookout-for-work-apps.md)
#### [Criar política de conformidade do Lookout](deploy-use/enable-device-threat-protection-rule-compliance-policy.md)
#### [Resolução de problemas de integração do Lookout](deploy-use/troubleshoot-lookout-integration.md)
#### [Monitorizar a Defesa Contra Ameaças para Dispositivos Móveis](deploy-use/monitor-mobile-threat-defense-compliance.md)

# Gestão de dispositivos móveis (MDM) no local
## [O que é a MDM no local](understand/manage-mobile-devices-with-on-premises-infrastructure.md)
## [Plano de MDM no local](plan-design/plan-on-premises-mdm.md)

## [Passos de configuração](get-started/preparation-steps-for-on-premises-mdm.md)
### [Configurar a subscrição do Intune](get-started/set-up-intune-subscription-on-premises-mdm.md)
### [Instalar funções no local](get-started/install-site-system-roles-for-on-premises-mdm.md)
### [Configurar certificados](get-started/set-up-certificates-on-premises-mdm.md)
### [Configurar para a inscrição](get-started/set-up-device-enrollment-on-premises-mdm.md)

## [Inscrever dispositivos para MDM no local](deploy-use/enroll-devices-on-premises-mdm.md)
### [Inscrição do utilizador](deploy-use/user-enroll-devices-on-premises-mdm.md)
### [Inscrição em massa](deploy-use/bulk-enroll-devices-on-premises-mdm.md)
## [Gerir dispositivos](deploy-use/onprem-manage-devices.md)
## [Gerir aplicações](deploy-use/onprem-manage-applications.md)
## [Proteger dados e dispositivos](deploy-use/onprem-protect-data-devices.md)

# [Gestão de dispositivos com o Exchange](deploy-use/manage-mobile-devices-with-exchange-activesync.md)