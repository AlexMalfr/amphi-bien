# AmphiBien

**Le “Tripadvisor” des amphis ! 🎓**

Site web full stack conçu par **[Alexandre MALFREYT](https://github.com/AlexMalfr)** & **[Julien ROSSE](https://github.com/JulienROSSE)** dans le cadre d'un cours de développement web en école d'ingénieurs.

![landing-video](https://github.com/user-attachments/assets/578926c7-d74b-46d6-9cc6-568467adcda4)

AmphiBien est un plateforme permettant aux étudiants de trouver, évaluer et signaler des problèmes dans les amphithéâtres de leur université. Les données sont créées de manière communautaire, fortement inspirée du fonctionnement de Google Maps.

📄 [Rapport de projet](./Rapport%20AmphiBien.pdf) · 📊 [Présentation](./Présentation%20AmphiBien.pdf)

---

## Aperçu

Page d'accueil

<img width="1814" height="983" alt="image" src="https://github.com/user-attachments/assets/380c397d-559f-4707-bd37-bfb66ef5460b" />


Liste des amphis avec carte

<img width="1815" height="982" alt="image" src="https://github.com/user-attachments/assets/5e6df521-0c44-4b0f-a00d-ca397e4f88df" />


Détail d'un amphi

<img width="1834" height="1694" alt="image" src="https://github.com/user-attachments/assets/0061f4a3-19e8-4dcb-843f-dcee9b42bf94" />


---

## Fonctionnalités

- 🗺️ Recherche d'amphis **à proximité** par géolocalisation
- 📋 Fiche détaillée : photos, équipements, carte interactive, capacité
- ⚠️ Signalement de problèmes (DANGER / PROBLÈME / NOTE) avec votes
- 🏫 Navigation par université
- 🔐 Authentification via Firebase (email + Google)
- ☁️ Upload et recadrage automatique des images via GCP Storage

---

## Charte graphique

Le design s'inspire d'**un brouillon sur feuille à carreaux** : papier ligné, polices manuscrites, éléments légèrement inclinés.

- Thème CSS : [Bootswatch Sketchy](https://bootswatch.com/sketchy/)
- Polices : **Cabin Sketch** (titres) & **Neucha** (corps de texte)

Prototype Figma (design mobile-first) :

![img80](https://github.com/user-attachments/assets/56a68d52-9d56-45ae-b5d1-a6b58c51936c)

---

## Stack technique

| Couche | Technologie |
|--------|-------------|
| Framework full-stack | [RedwoodJS](https://redwoodjs.com/) |
| Langage | TypeScript |
| Frontend | React 18 |
| Styling | Tailwind CSS + Bootstrap (Sketchy) |
| API | GraphQL (GraphQL Yoga) |
| ORM | Prisma |
| Base de données | PostgreSQL (prod) / SQLite (dev) |
| Authentification | Firebase Authentication |
| Stockage images | Google Cloud Storage + Cloud Functions |
| Carte | Leaflet + OpenStreetMap |
| Hébergement | Google Cloud Run (serverless) |
| Nom de domaine | amphi-bien.fr (OVH → GCP Load Balancer) |
| Versioning | Git / GitHub |

---
---
---
---
---
---

# README par défaut RedWoodJS

Welcome to [RedwoodJS](https://redwoodjs.com)!

> **Prerequisites**
>
> - Redwood requires [Node.js](https://nodejs.org/en/) (=20.x) and [Yarn](https://yarnpkg.com/)
> - Are you on Windows? For best results, follow our [Windows development setup](https://redwoodjs.com/docs/how-to/windows-development-setup) guide

Start by installing dependencies:

```
yarn install
```

Then start the development server:

```
yarn redwood dev
```

Your browser should automatically open to [http://localhost:8910](http://localhost:8910) where you'll see the Welcome Page, which links out to many great resources.

> **The Redwood CLI**
>
> Congratulations on running your first Redwood CLI command! From dev to deploy, the CLI is with you the whole way. And there's quite a few commands at your disposal:
>
> ```
> yarn redwood --help
> ```
>
> For all the details, see the [CLI reference](https://redwoodjs.com/docs/cli-commands).

## Prisma and the database

Redwood wouldn't be a full-stack framework without a database. It all starts with the schema. Open the [`schema.prisma`](api/db/schema.prisma) file in `api/db` and replace the `UserExample` model with the following `Post` model:

```prisma
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  body      String
  createdAt DateTime @default(now())
}
```

Redwood uses [Prisma](https://www.prisma.io/), a next-gen Node.js and TypeScript ORM, to talk to the database. Prisma's schema offers a declarative way of defining your app's data models. And Prisma [Migrate](https://www.prisma.io/migrate) uses that schema to make database migrations hassle-free:

```
yarn rw prisma migrate dev

# ...

? Enter a name for the new migration: › create posts
```

> `rw` is short for `redwood`

You'll be prompted for the name of your migration. `create posts` will do.

Now let's generate everything we need to perform all the CRUD (Create, Retrieve, Update, Delete) actions on our `Post` model:

```
yarn redwood generate scaffold post
```

Navigate to [http://localhost:8910/posts/new](http://localhost:8910/posts/new), fill in the title and body, and click "Save".

Did we just create a post in the database? Yup! With `yarn rw generate scaffold <model>`, Redwood created all the pages, components, and services necessary to perform all CRUD actions on our posts table.

## Frontend first with Storybook

Don't know what your data models look like? That's more than ok—Redwood integrates Storybook so that you can work on design without worrying about data. Mockup, build, and verify your React components, even in complete isolation from the backend:

```
yarn rw storybook
```

Seeing "Couldn't find any stories"? That's because you need a `*.stories.{tsx,jsx}` file. The Redwood CLI makes getting one easy enough—try generating a [Cell](https://redwoodjs.com/docs/cells), Redwood's data-fetching abstraction:

```
yarn rw generate cell examplePosts
```

The Storybook server should hot reload and now you'll have four stories to work with. They'll probably look a little bland since there's no styling. See if the Redwood CLI's `setup ui` command has your favorite styling library:

```
yarn rw setup ui --help
```

## Testing with Jest

It'd be hard to scale from side project to startup without a few tests. Redwood fully integrates Jest with both the front- and back-ends, and makes it easy to keep your whole app covered by generating test files with all your components and services:

```
yarn rw test
```

To make the integration even more seamless, Redwood augments Jest with database [scenarios](https://redwoodjs.com/docs/testing#scenarios) and [GraphQL mocking](https://redwoodjs.com/docs/testing#mocking-graphql-calls).

## Ship it

Redwood is designed for both serverless deploy targets like Netlify and Vercel and serverful deploy targets like Render and AWS:

```
yarn rw setup deploy --help
```

Don't go live without auth! Lock down your app with Redwood's built-in, database-backed authentication system ([dbAuth](https://redwoodjs.com/docs/authentication#self-hosted-auth-installation-and-setup)), or integrate with nearly a dozen third-party auth providers:

```
yarn rw setup auth --help
```

## Next Steps

The best way to learn Redwood is by going through the comprehensive [tutorial](https://redwoodjs.com/docs/tutorial/foreword) and joining the community (via the [Discourse forum](https://community.redwoodjs.com) or the [Discord server](https://discord.gg/redwoodjs)).

## Quick Links

- Stay updated: read [Forum announcements](https://community.redwoodjs.com/c/announcements/5), follow us on [Twitter](https://twitter.com/redwoodjs), and subscribe to the [newsletter](https://redwoodjs.com/newsletter)
- [Learn how to contribute](https://redwoodjs.com/docs/contributing)
