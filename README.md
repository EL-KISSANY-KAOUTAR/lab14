# LAB 14 : Bypass Root Detection sur Android : Techniques Dynamiques avec Frida, Objection et Hooks Natifs

## Objectif du laboratoire

L'objectif de ce laboratoire est d'étudier les mécanismes de détection de root implémentés dans les applications Android et de mettre en œuvre différentes techniques de contournement (bypass) à l'aide d'outils d'analyse dynamique tels que **Frida**, **Objection** et des **hooks natifs**.

---

# 1. Préparation de l'environnement

## 1.1 Installation de Python et des outils Frida

Installer Python puis les outils Frida sur le poste d'analyse :

```bash
pip install frida-tools
```

Vérifier l'installation :

```bash
frida --version
```

### Vérification

![Installation Frida](https://github.com/user-attachments/assets/f2a148c5-ea63-40ca-be24-156c2d067848)

---

## 1.2 Installation d'ADB (Android Platform Tools)

Télécharger les Android Platform Tools :

https://developer.android.com/tools/releases/platform-tools

Vérifier l'installation :

```bash
adb version
```

### Vérification 

![ADB Installation](https://github.com/user-attachments/assets/5e7ce59c-227e-4782-9c23-90fcc34791f5)

---

# 2. Démarrage de Frida Server sur Android

Afin de permettre à Frida, Objection et Medusa d'interagir avec l'appareil Android, il est nécessaire de lancer **frida-server** sur l'émulateur ou l'appareil physique.

Après avoir déployé et lancé **frida-server**, vérifier la connexion avec :

```bash
frida-ps -Uai
```

Cette commande liste toutes les applications et processus présents sur l'appareil Android connecté.

### Résultat obtenu

![Liste des applications](https://github.com/user-attachments/assets/acbf2790-ddfc-4c31-9633-d0cc2826be1f)

![Liste des processus](https://github.com/user-attachments/assets/95eed3f1-37ca-4c91-8cb7-09ea2a22533b)

---

# 3. Bypass Root Detection avec Frida

L'approche la plus courante consiste à injecter un script Frida dans l'application afin d'intercepter les appels utilisés pour détecter :

- Magisk
- SuperSU
- BusyBox
- RootBeer
- Présence du binaire `su`
- Vérifications système

Exemple d'injection :

```bash
frida -U -f com.example.application -l root_bypass.js
```

Une fois le script chargé, les mécanismes de détection de root sont neutralisés dynamiquement.

---

# 4. Bypass Root Detection avec Objection

Objection est un framework construit au-dessus de Frida permettant d'effectuer des opérations courantes sans écrire de scripts.

## Lancement d'Objection

```bash
objection -g com.example.application explore
```

### Connexion réussie

![Connexion Objection](https://github.com/user-attachments/assets/a88b146a-2d84-4dc4-aac7-edd9b4ab0ad0)

---

## Désactivation de la détection de Root

Une fois connecté à l'application :

```bash
android root disable
```

Cette commande applique automatiquement plusieurs hooks Frida destinés à contourner les mécanismes de détection de root.

### Exécution du bypass

![Root Disable](https://github.com/user-attachments/assets/3baf6135-ba9a-4bf1-a9ec-0d61a6133145)

---

## Vérification

Après exécution du bypass, l'application ne détecte plus l'environnement rooté et continue normalement son exécution.

### Résultat obtenu

![Bypass réussi](https://github.com/user-attachments/assets/775799f5-02ac-4586-b6a8-7b267af4866d)

---

---

# Conclusion

Au cours de ce laboratoire, nous avons préparé l'environnement d'analyse dynamique Android et mis en œuvre plusieurs techniques permettant de contourner les mécanismes de détection de root. Les outils **Frida** et **Objection** offrent des méthodes efficaces pour neutraliser ces protections et faciliter l'analyse de sécurité des applications Android.




