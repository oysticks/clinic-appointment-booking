# Clinic appointment booking

Online booking for one small clinic. Patients find a time that is
really free and book it themselves. The front desk (the clinic's
reception staff) sees the whole day on one screen. Nobody arrives to
find their time was given to somebody else.

## What finished looks like

Anyone can open the site and:

- create an account and confirm their email address
- book an appointment at a time that is really free
- get a reminder while they can still cancel
- cancel or move the appointment without phoning anybody

The clinic's staff open their own screen and see the whole day.

Finished means it is live on the internet, not just on your laptop.
Someone you have never met can use it on their own phone.

## The road map

Eight sprints. Each sprint delivers one part of the list above. They
must be done in order, because each one builds on the one before.

| # | Sprint | What it delivers |
|---|---|---|
| 1 | Getting in | Patients create an account and come back to it. Staff accounts exist, and nobody can give themselves one |
| 2 | The diary | The clinic sets its opening hours. A patient books a free time, and two patients can never get the same time |
| 3 | Two sides of the desk | Staff see the whole day. A patient sees only their own appointments |
| 4 | Changing plans | Patients cancel or move an appointment, and the freed time goes back on offer |
| 5 | Reminders people act on | Patients get a reminder while they can still cancel, and can turn reminders off |
| 6 | Work that runs itself | Reminders go out on time with nobody pressing a button, and never twice |
| 7 | Opening the doors | A new patient proves the email address is theirs before they can book |
| 8 | Put it where people are | The site is live on the internet at its own address |

## The hard part

Two patients tap the last free time on Tuesday at the same moment.
Only one of them can have it. Sprint 2 solves this. A simple check in
the code ("is this time still free?") is not enough, because both
requests can pass the check before either one saves. You will prove
this by making two bookings race each other.

## Working on it

The sprints, their briefs and their tickets are in Blacksmith
Experience. Start with sprint 1. Each sprint opens when the one before
it is finished.

Read the documents attached to a sprint before you start its first
ticket. They explain the choices you will make and the options you are
choosing between.

## What this is built with

The whole product: an API and the screens that use it.

- **Django** with **Django REST Framework** for the API.
- **SimpleJWT** for authentication, against a custom user model in `apps/users`.
- **drf-spectacular** for the OpenAPI schema, served at `/api/schema/` and browsable at `/api/docs/`.
- **React** with **Vite** for the dev server and the build.
- **Chakra UI** for components, and **React Router** for routes.
- **TanStack Query** for every call to the API, so caching and refetching are decided in one place.

## Setting it up

You need the CLI once: `npm install -g blacksmith-cli`.

```bash
blacksmith setup     # dependencies, database, migrations
blacksmith dev       # start it
```

The API answers on `http://localhost:8000`, and the app on `http://localhost:5173`.

Copy `backend/.env.example` to `backend/.env` before the first run. It is ignored by git and holds the secret key, the database URL and anything else this project should not carry in its history.

## Where the code lives

```
backend/
├── config/
│   ├── settings/        # base, development, production
│   └── urls.py          # where routes are mounted
├── apps/
│   └── users/           # the custom user model, and auth
├── utils/               # shared helpers, base model
├── manage.py
└── requirements.txt

frontend/
└── src/
    ├── api/
    │   ├── generated/   # written by `blacksmith sync` — do not edit
    │   └── hooks/       # your queries and mutations
    ├── pages/           # one folder per page
    ├── features/        # auth, and anything else that spans pages
    ├── router/          # routes and layouts
    ├── shared/          # components and hooks used across pages
    └── styles/
```

## Day to day

| Command | What it does |
| --- | --- |
| `blacksmith dev` | Run it locally. |
| `blacksmith sync` | Regenerate the frontend API types and hooks from the backend schema. Run it after changing a serializer or a route. |
| `blacksmith make:resource Post` | Scaffold a model, serializer, viewset and routes, plus the hooks and pages that use them. |
| `blacksmith backend <command>` | Run a Django management command, e.g. `blacksmith backend createsuperuser`. |
| `blacksmith frontend <command>` | Run an npm command in the frontend, e.g. `blacksmith frontend install axios`. |
| `blacksmith eject` | Remove Blacksmith and keep a plain Django and React project. Nothing here is a dependency on us. |
