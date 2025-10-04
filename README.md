# 👻 Module de Sécurité Ghost
**Outil de Durcissement de Sécurité Windows & Azure basé sur PowerShell**

> **Durcissement proactif de la sécurité pour les points de terminaison Windows et les environnements Azure.** Ghost fournit des fonctions de durcissement basées sur PowerShell qui peuvent aider à réduire les vecteurs d'attaque courants en désactivant les services et protocoles inutiles.

## ⚠️ Avertissements Importants

**TESTS REQUIS** : Testez toujours Ghost dans des environnements de non-production d'abord. La désactivation de services peut impacter les fonctions métier légitimes.

**AUCUNE GARANTIE** : Bien que Ghost cible les vecteurs d'attaque courants, aucun outil de sécurité ne peut prévenir toutes les attaques. Ceci est un composant d'une stratégie de sécurité complète.

**IMPACT OPÉRATIONNEL** : Certaines fonctions peuvent affecter la fonctionnalité du système. Examinez attentivement chaque paramètre avant le déploiement.

**ÉVALUATION PROFESSIONNELLE** : Pour les environnements de production, consultez des professionnels de la sécurité pour vous assurer que les paramètres correspondent aux besoins de votre organisation.

## 📊 Le Paysage de la Sécurité

Les dommages causés par les rançongiciels ont atteint **57 milliards de dollars en 2025**, et les recherches indiquent que de nombreuses attaques réussies exploitent les services Windows de base et les mauvaises configurations. Les vecteurs d'attaque courants incluent :

- **90% des incidents de rançongiciels** impliquent l'exploitation RDP
- **Les vulnérabilités SMBv1** ont permis des attaques comme WannaCry et NotPetya
- **Les macros de documents** restent une méthode principale de livraison de malware
- **Les attaques basées sur USB** continuent de cibler les réseaux isolés
- **L'abus de PowerShell** a considérablement augmenté ces dernières années

## 🛡️ Fonctions de Sécurité Ghost

Ghost fournit **16 fonctions de durcissement Windows** plus **l'intégration de sécurité Azure** :

### Durcissement des Points de Terminaison Windows

| Fonction | Objectif | Considérations |
|----------|----------|----------------|
| `Set-RDP` | Gère l'accès Bureau à distance | Peut impacter l'administration à distance |
| `Set-SMBv1` | Contrôle le protocole SMB hérité | Requis pour les très anciens systèmes |
| `Set-AutoRun` | Contrôle AutoPlay/AutoRun | Peut impacter la commodité utilisateur |
| `Set-USBStorage` | Restreint les périphériques de stockage USB | Peut impacter l'usage USB légitime |
| `Set-Macros` | Contrôle l'exécution des macros Office | Peut impacter les documents avec macros |
| `Set-PSRemoting` | Gère la communication à distance PowerShell | Peut impacter la gestion à distance |
| `Set-WinRM` | Contrôle Windows Remote Management | Peut affecter l'administration à distance |
| `Set-LLMNR` | Gère le protocole de résolution de noms | Généralement sûr à désactiver |
| `Set-NetBIOS` | Contrôle NetBIOS sur TCP/IP | Peut affecter les applications héritées |
| `Set-AdminShares` | Gère les partages administratifs | Peut impacter l'accès aux fichiers distants |
| `Set-Telemetry` | Contrôle la collecte de données | Peut affecter les capacités de diagnostic |
| `Set-GuestAccount` | Gère le compte Invité | Généralement sûr à désactiver |
| `Set-ICMP` | Contrôle les réponses ping | Peut affecter les diagnostics réseau |
| `Set-RemoteAssistance` | Gère l'Assistance à distance | Peut impacter les opérations du support technique |
| `Set-NetworkDiscovery` | Contrôle la découverte réseau | Peut affecter la navigation réseau |
| `Set-Firewall` | Gère le Pare-feu Windows | Critique pour la sécurité réseau |

### Sécurité Cloud Azure

| Fonction | Objectif | Exigences |
|----------|----------|-----------|
| `Set-AzureSecurityDefaults` | Active la sécurité de base Azure AD | Permissions Microsoft Graph |
| `Set-AzureConditionalAccess` | Configure les politiques d'accès | Licences Azure AD P1/P2 |
| `Set-AzurePrivilegedUsers` | Audite les comptes privilégiés | Permissions Administrateur Global |

### Options de Déploiement Entreprise

| Méthode | Cas d'usage | Exigences |
|---------|-------------|-----------|
| **Exécution Directe** | Tests, petits environnements | Droits d'administrateur local |
| **Group Policy** | Environnements de domaine | Administrateur de domaine, gestion GP |
| **Microsoft Intune** | Appareils gérés dans le cloud | Licences Intune, API Graph |

## 🚀 Démarrage Rapide

### Évaluation de Sécurité
```powershell
# Charger le module Ghost
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Vérifier la posture de sécurité actuelle
Get-Ghost
```

### Durcissement de Base (Testez d'abord)
```powershell
# Durcissement essentiel - testez d'abord en environnement de laboratoire
Set-Ghost -SMBv1 -AutoRun -Macros

# Examiner les changements
Get-Ghost
```

### Déploiement Entreprise
```powershell
# Déploiement Group Policy (environnements de domaine)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Déploiement Intune (appareils gérés dans le cloud)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Méthodes d'Installation

### Option 1 : Téléchargement Direct (Tests)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Option 2 : Installation de Module
```powershell
# Installer depuis PowerShell Gallery (quand disponible)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Option 3 : Déploiement Entreprise
```powershell
# Copier vers un emplacement réseau pour le déploiement Group Policy
# Configurer les scripts PowerShell Intune pour le déploiement cloud
```

## 💼 Exemples de Cas d'Usage

### Petite Entreprise
```powershell
# Protection de base avec impact minimal
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Environnement de Santé
```powershell
# Durcissement axé HIPAA
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Services Financiers
```powershell
# Configuration haute sécurité
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Organisation Cloud-First
```powershell
# Déploiement géré par Intune
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 📝 Détails des Fonctions

### Fonctions de Durcissement Principal

#### Services Réseau
- **RDP** : Bloque l'accès bureau à distance ou randomise le port
- **SMBv1** : Désactive le protocole de partage de fichiers hérité
- **ICMP** : Empêche les réponses ping pour la reconnaissance
- **LLMNR/NetBIOS** : Bloque les protocoles de résolution de noms hérités

#### Sécurité des Applications
- **Macros** : Désactive l'exécution de macros dans les applications Office
- **AutoRun** : Empêche l'exécution automatique depuis les médias amovibles

#### Gestion à Distance
- **PSRemoting** : Désactive les sessions PowerShell à distance
- **WinRM** : Arrête Windows Remote Management
- **Assistance à Distance** : Bloque les connexions d'assistance à distance

#### Contrôle d'Accès
- **Partages Admin** : Désactive les partages C$, ADMIN$
- **Compte Invité** : Désactive l'accès du compte Invité
- **Stockage USB** : Restreint l'utilisation des périphériques USB

### Intégration Azure
```powershell
# Se connecter au tenant Azure
Connect-AzureGhost -Interactive

# Activer les paramètres de sécurité par défaut
Set-AzureSecurityDefaults -Enable

# Configurer l'accès conditionnel
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Auditer les utilisateurs privilégiés
Set-AzurePrivilegedUsers -AuditOnly
```

### Intégration Intune (Nouveau dans v2)
```powershell
# Se connecter à Intune
Connect-IntuneGhost -Interactive

# Déployer via les politiques Intune
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Considérations Importantes

### Exigences de Test
- **Environnement de Laboratoire** : Testez tous les paramètres dans un environnement isolé d'abord
- **Déploiement Phasé** : Déployez progressivement pour identifier les problèmes
- **Plan de Retour Arrière** : Assurez-vous de pouvoir annuler les changements si nécessaire
- **Documentation** : Enregistrez quels paramètres fonctionnent pour votre environnement

### Impact Potentiel
- **Productivité Utilisateur** : Certains paramètres peuvent affecter les flux de travail quotidiens
- **Applications Héritées** : Les systèmes plus anciens peuvent nécessiter certains protocoles
- **Accès à Distance** : Considérez l'impact sur l'administration à distance légitime
- **Processus Métier** : Vérifiez que les paramètres ne cassent pas les fonctions critiques

### Limitations de Sécurité
- **Défense en Profondeur** : Ghost est une couche de sécurité, pas une solution complète
- **Gestion Continue** : La sécurité nécessite une surveillance et des mises à jour continues
- **Formation Utilisateur** : Les contrôles techniques doivent être associés à la sensibilisation à la sécurité
- **Évolution des Menaces** : Les nouvelles méthodes d'attaque peuvent contourner les protections actuelles

## 🎯 Exemples de Scénarios d'Attaque

Bien que Ghost cible les vecteurs d'attaque courants, la prévention spécifique dépend de la mise en œuvre et des tests appropriés :

### Attaques de Type WannaCry
- **Atténuation** : `Set-Ghost -SMBv1` désactive le protocole vulnérable
- **Considération** : Assurez-vous qu'aucun système hérité ne nécessite SMBv1

### Rançongiciels Basés sur RDP
- **Atténuation** : `Set-Ghost -RDP` bloque l'accès bureau à distance
- **Considération** : Peut nécessiter des méthodes d'accès à distance alternatives

### Malware Basé sur Documents
- **Atténuation** : `Set-Ghost -Macros` désactive l'exécution de macros
- **Considération** : Peut impacter les documents légitimes avec macros

### Menaces Livrées par USB
- **Atténuation** : `Set-Ghost -USBStorage -AutoRun` restreint la fonctionnalité USB
- **Considération** : Peut impacter l'utilisation légitime des périphériques USB

## 🏢 Fonctionnalités Entreprise

### Support Group Policy
```powershell
# Appliquer les paramètres via le registre Group Policy
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Les paramètres s'appliquent à l'échelle du domaine après actualisation GP
gpupdate /force
```

### Intégration Microsoft Intune
```powershell
# Créer des politiques Intune pour les paramètres Ghost
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Les politiques se déploient automatiquement sur les appareils gérés
```

### Rapports de Conformité
```powershell
# Générer un rapport d'évaluation de sécurité
Get-Ghost | Export-Csv -Path "AuditSecurite-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Rapport de posture de sécurité Azure
Get-AzureGhost | Out-File "RapportSecuriteAzure.txt"
```

## 📚 Meilleures Pratiques

### Pré-déploiement
1. **Documenter l'État Actuel** : Exécutez `Get-Ghost` avant les changements
2. **Tester Minutieusement** : Validez dans un environnement de non-production
3. **Planifier le Retour Arrière** : Sachez comment annuler chaque paramètre
4. **Revue des Parties Prenantes** : Assurez-vous que les unités métier approuvent les changements

### Pendant le Déploiement
1. **Approche Phasée** : Déployez d'abord vers les groupes pilotes
2. **Surveiller l'Impact** : Surveillez les plaintes des utilisateurs ou les problèmes système
3. **Documenter les Problèmes** : Enregistrez tous les problèmes pour référence future
4. **Communiquer les Changements** : Informez les utilisateurs des améliorations de sécurité

### Post-déploiement
1. **Évaluation Régulière** : Exécutez périodiquement `Get-Ghost` pour vérifier les paramètres
2. **Mettre à Jour la Documentation** : Maintenez les configurations de sécurité à jour
3. **Examiner l'Efficacité** : Surveillez les incidents de sécurité
4. **Amélioration Continue** : Ajustez les paramètres selon le paysage des menaces

## 🔧 Dépannage

### Problèmes Courants
- **Erreurs de Permission** : Assurez-vous d'une session PowerShell élevée
- **Dépendances de Service** : Certains services peuvent avoir des dépendances
- **Compatibilité d'Application** : Testez avec les applications métier
- **Connectivité Réseau** : Vérifiez que l'accès à distance fonctionne toujours

### Options de Récupération
```powershell
# Réactiver des services spécifiques si nécessaire
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 À Propos de l'Auteur

**Jim Tyler** - Microsoft MVP pour PowerShell
- **YouTube** : [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10 000+ abonnés)
- **Newsletter** : [PowerShell.News](https://powershell.news) - Intelligence de sécurité hebdomadaire
- **Auteur** : "PowerShell for Systems Engineers"
- **Expérience** : Décennies d'automatisation PowerShell et de sécurité Windows

## 📄 Licence & Avertissement

### Licence MIT
Ghost est fourni sous licence MIT pour une utilisation, modification et distribution libres.

### Avertissement de Sécurité
- **Aucune Garantie** : Ghost est fourni "tel quel" sans garantie d'aucune sorte
- **Tests Requis** : Testez toujours dans des environnements de non-production d'abord
- **Guidance Professionnelle** : Consultez des professionnels de la sécurité pour les déploiements de production
- **Impact Opérationnel** : Les auteurs ne sont pas responsables de toute perturbation opérationnelle
- **Sécurité Complète** : Ghost est un composant d'une stratégie de sécurité complète

### Support
- **GitHub Issues** : [Signaler des bugs ou demander des fonctionnalités](https://github.com/jimrtyler/Ghost/issues)
- **Documentation** : Utilisez `Get-Help <fonction> -Full` pour une aide détaillée
- **Communauté** : Forums de la communauté PowerShell et sécurité

---

**🔒 Renforcez votre posture de sécurité avec Ghost - mais testez toujours d'abord.**

```powershell
# Commencez par l'évaluation, pas les suppositions
Get-Ghost
```

**⭐ Donnez une étoile à ce dépôt si Ghost aide à améliorer votre posture de sécurité !**