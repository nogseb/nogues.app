# nogues.app

Page d'accueil de [nogues.app](https://nogues.app/) : « Bricolages », un carnet des expérimentations web et IA générative de Sébastien Noguès.

## Structure

```
site/                  contenu publié à la racine du domaine (www/)
  index.html           page d'accueil autonome (HTML et CSS, sans dépendance de build)
  .htaccess            sert index.html en priorité
.github/workflows/
  deploy-ovh.yml       publication automatique en SFTP sur l'hébergement OVHcloud
```

## Ajouter une expérience

Dans `site/index.html`, dupliquer un bloc `<li class="card ..."> ... </li>` de la section Expériences et adapter la catégorie, le titre, le lien, la description, le statut et les outils. Catégories disponibles (classe et couleur) : `veille`, `explo`, `travail`, `perso`. Un projet privé reçoit en plus la classe `prive` et un titre sans lien.

## Publication

Le workflow envoie `site/` dans `www/` à chaque modification poussée sur `main`, ou à la demande (onglet Actions → « Publier nogues.app sur OVHcloud » → Run workflow).

Les secrets GitHub sont propres à chaque dépôt : ceux du dépôt `reunion` ne sont pas visibles ici. À créer dans **Settings → Secrets and variables → Actions** de ce dépôt :

| Nom | Type | Valeur |
|---|---|---|
| `OVH_SFTP_HOST` | secret | serveur FTP/SFTP (espace client OVHcloud, onglet « FTP - SSH ») |
| `OVH_SFTP_USER` | secret | login FTP, avec la case SFTP cochée |
| `OVH_SFTP_PASSWORD` | secret | mot de passe FTP |
| `OVH_TARGET_DIR` | variable (facultative) | dossier cible, `www` par défaut |

Le workflow ajoute ou remplace des fichiers et n'en supprime jamais : les sous-dossiers publiés par d'autres dépôts (comme `www/rm`) ne sont pas touchés.

Prérequis : certificat SSL actif pour nogues.app (onglet Multisite de l'hébergement). Le `.app` n'est ouvert par les navigateurs qu'en HTTPS.
