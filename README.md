1. Installation du rôle Serveur de fichiers

Install-WindowsFeature -Name FS-FileServer -IncludeManagementTools


2. Création du dossier partagé

New-Item -Path "C:\Documents_Entreprise" -ItemType Directory
New-Item -Path "C:\Documents_Entreprise\RH" -ItemType Directory
New-Item -Path "C:\Documents_Entreprise\Comptabilité" -ItemType Directory
New-Item -Path "C:\Documents_Entreprise\Direction" -ItemType Directory


3. Configuration du partage

New-SmbShare -Name "Docs" -Path "C:\Documents_Entreprise" -FullAccess "Administrateurs" -ReadAccess "Utilisateurs du domaine"


4. Configuration des permissions NTFS

icacls "C:\Documents_Entreprise\RH" /grant RH:M
icacls "C:\Documents_Entreprise\Comptabilité" /grant Comptabilité:M
icacls "C:\Documents_Entreprise\Direction" /grant Direction:M
icacls "C:\Documents_Entreprise" /grant "Utilisateurs du domaine":R


5. Vérification des partages

Get-SmbShare


6. Configuration du lecteur réseau sur un client

New-PSDrive -Name "Z" -PSProvider FileSystem -Root "\\serveur\Docs" -Persist

