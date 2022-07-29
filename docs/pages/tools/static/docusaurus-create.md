# Create doc with Docusaurus in GitLab Pages

2022-02-25

- Here the  [Docusaurus docs](https://docusaurus.io/) et [GitLab Pages docs](https://docs.gitlab.com/ee/user/project/pages/).

- Create a **Docusaurus** project

```bash
$ npx create-docusaurus@latest <your-repo> classic
$ npm install @cmfcmf/docusaurus-search-local
```

Add to `docusaurus.config.js` file before themeConfig:

```js
// ...
plugins: [
    [
      require.resolve("@cmfcmf/docusaurus-search-local"),
      {
        language: "fr",
      }
    ],
  ],
themeConfig:
// ...
```

Create the build and test the search with serve :

```bash
$ npm run build
$ npm run serve
```

- Go in repo

```shell
cd <your-repo>
```

- And start the dev

```bash
$ npx docusaurus start
# or npm run start
```

## Custom project

### All are in *docusaurus.config.js* file

- Change the **title** and **tagline**

```js
const config = {
  title: 'YoanDev Doc',
  tagline: 'Documenter c\'est cool !',
```

- Change the menu and logo:

```js
navbar: {
  title: 'YoanDev Doc',
  logo: {
    alt: 'My Site Logo',
    src: 'img/logo.svg',
  },
```

- Change the copyright in footer

```js
copyright: `Copyright © ${new Date().getFullYear()} YoanDev Doc. Built with Docusaurus.`,
```

### Change the style with : *`src/css/custom.css`*

> Here a style generator :  [Styling layout in Docusaurus](https://docusaurus.io/docs/styling-layout#styling-your-site-with-infima).

- Change **dark** theme:

```scss
[data-theme='dark'] {
  --ifm-color-primary: #b3dde6;
  --ifm-color-primary-dark: #94cfdc;
  --ifm-color-primary-darker: #85c8d7;
  --ifm-color-primary-darkest: #57b4c8;
  --ifm-color-primary-light: #d2ebf0;
  --ifm-color-primary-lighter: #e1f2f5;
  --ifm-color-primary-lightest: #ffffff;
}
```

- **light** theme:

```scss
:root {
  --ifm-color-primary: #043c48;
  --ifm-color-primary-dark: #043641;
  --ifm-color-primary-darker: #03333d;
  --ifm-color-primary-darkest: #032a32;
  --ifm-color-primary-light: #04424f;
  --ifm-color-primary-lighter: #054553;
  --ifm-color-primary-lightest: #054e5e;
}
```

## Change Doc content

### Supress *Blog*

> 2 steps

- Delete `blog` directory
- and remove  link in `docusaurus.config.js` file:

```js
// header menu
{to: '/blog', label: 'Blog', position: 'left'},

// in footer
{
  label: 'Blog',
  to: '/blog',
},
```

### Produce content

**Add a new section**

- For exemple create a `docs/efx-doc` directory
- Create a file : `_category_.json` to the root of efx-doc directory :

```json
{
  "label": "YoanDev - Doc",
  "position": 4
}
```

- And add a markdown `demo.md` file

```markdown
  ---
  sidebar_position: 1
  ---

  # Ceci est un H1

  ## Ceci est un H2

  ### Ceci est un H3

  **Texte en gras**

  *Texte en italique*

  Ceci est une liste :

  * Lorem
  * ipsum

  > Ceci est un citation

  :::danger Ceci est le titre du bloc !
  Ceci est un blog de **danger**
  :::

  :::success
  Ceci est un blog de **success**
  :::
```

- Doc are available :

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-19-18-33-47.png)

### Add a extension theme syntax add-on, e.g. `php`

- Open `docusaurus.config.js` and add:

```js
prism: {
  theme: lightCodeTheme,
  darkTheme: darkCodeTheme,
  // Ajoutons le php avec cette ligne
  additionalLanguages: ['php'],
},
```

## GitLab Pages

### Create the repo

> Create a **free** account on [GitLab.com](https://gitlab.com/)

- Create a GitLab repo
- Do a `git push` on it

### Add a pipe deployment

> La publication de notre Docusaurus sera piloter par un pipeline GitLab CI (Et si les pipeline CI/CD vous interesse, vous pouvez jetter un cop d’oeil à ma [formation sur le sujet](https://formation.yoandev.co/ci-cd-pour-les-devs-php-avec-gitlab-ci-et-github-actions))

- Création d’un fichier `.gitlab-ci.yml` à la racine du projet, avec le contenu suivant:

```yaml
image: node:15.12-alpine3.13

stages:
  - test
  - deploy

test:
  stage: test
  script:
    - npm install --force
    - npm run build

pages:
  stage: deploy
  script:
    - npm install --force
    - npm run build
    - mv ./build ./public
  artifacts:
    paths:
    - public
  only:
    - pages
```

- Ce fichier, va faire les choses suivantes :
  
  - Lors d’un push: lancer un `npm run build` pour vérifier que le build fonctionne bien
  - Lors d’un push, ou merge request sur la branche **pages**: lancer le build et générer un artefact avec la version statique de notre Docusaurus

- On **commit** et on **push**

### La branche *pages*

- Créons la branche **pages** depuis GitLab (cela devrait immédiatement lancer le pipeline de déploiement)

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-22-15-39-17.png)

- Une fois la CI/CD exécutée, dans **Settings > Pages**, activons le **https** et faisons un **save changes**

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-22-15-47-19.png)

- Et testons la page (*l’obtebtion du certificat pour le HTTPS peut ne pas être immédiat !*)

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-22-15-50-43.png)

### Adpatons le projet à notre dépot GitLab

- Modifions notre fichier `docusaurus.config.js` avec les adresses de notre dépot

```js
const config = {
  title: 'YoanDev Doc',
  tagline: 'Documenter c\'est cool !',
  url: 'https://yoandev.co.gitlab.io',
  baseUrl: '/yoandev-doc-prepa/',
  onBrokenLinks: 'throw',
  onBrokenMarkdownLinks: 'warn',
  favicon: 'img/favicon.ico',
  organizationName: 'yoandev', // Usually your GitHub org/user name.
  projectName: 'yoandev-doc-prepa', // Usually your repo name.

  presets: [
    [
      'classic',
      /** @type {import('@docusaurus/preset-classic').Options} */
      ({
        docs: {
          sidebarPath: require.resolve('./sidebars.js'),
          // Please change this to your repo.
          editUrl: 'https://gitlab.com/yoandev.co/yoandev-doc-prepa/-/edit/master/',
        },
        blog: {
          showReadingTime: true,
          // Please change this to your repo.
          editUrl:
            'https://gitlab.com/yoandev.co/yoandev-doc-prepa/-/edit/master/',
        },
        theme: {
          customCss: require.resolve('./src/css/custom.css'),
        },
      }),
    ],
  ],
```

- Et faisons une **Merge Request** de **Master** vers **Pages**, et constatons le résultat 🚀

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-22-16-13-06.png)

## BONUS : Ajoutons un *moteur de recherche*

> Il existe des solutions plus performante pour mettre en place un moteur de recherche, mais celle-ci à le bon gout de fonctionner simplement, rapidement, y compris pour un dépot privé (et donc un GitLab Pages non accessible à tous le monde)

- Installons la dépendance [docusaurus-serach-local](https://github.com/cmfcmf/docusaurus-search-local)

```shell
npm install
npm install @cmfcmf/docusaurus-search-local
```

- Ajoutons la recherche dans le fichier `docusaurus.config.js`

```js
// ...
plugins: [
    [
      require.resolve("@cmfcmf/docusaurus-search-local"),
      {
        language: "fr",
      }
    ],
  ],
themeConfig:
// ...
```

- Et finalement testons

```shell
npm run build
npm run serve
```

![](https://yoandev.co/une-documentation-avec-docusaurus-et-gitlab-pages/img/2022-02-22-16-23-40.png)

- Il ne nous reste qu’à commit + push + MR sur la branche pages !

## Conclusions

Nous venons de voir comment mettre en ligne hyper simplement un site statique de documentation à l’aide de plusieurs outils : Docusaurus, Gitlab CI et GitLab Pages !

Vous n’avez plus aucunes excuse pour ne pas écrire et partager de la documentations avec vos collègues (vous devriez vous faire des plateformes de doc !), pour vos clients ou vos utilisateurs !

Nous allons poursuivre prochainement notre découverte des outils de génération de sites statique (jamstack) avec un générateur super cool pour un blog… rendez vous bientôt !
