# Keycloak boilerplate

Keep your own Keycloak themes and providers in Git and deploy them with Wodby.

Use it with the [buildable Keycloak](https://github.com/wodby/service-keycloak-buildable)
service (`keycloak-buildable`). For Keycloak without your own themes or
providers, use the [Keycloak](https://github.com/wodby/service-keycloak)
service instead.

## Keycloak's version

Choose the Keycloak version for the service when you create the app. The build
starts from the official Keycloak image of that version, adds your themes and
providers, and runs Keycloak's build. Your providers must support that version.

## Themes

Put each theme in its own directory under `themes/`, with a directory per
theme type holding its `theme.properties`:

```
themes/
  my-theme/
    login/
      theme.properties
      resources/css/my-theme.css
```

A `login/theme.properties` that extends Keycloak's theme can start with:

```
parent=keycloak.v2
import=common/keycloak
styles=css/login.css css/my-theme.css
```

Select the theme for a realm in Keycloak's administration console, under
**Realm settings > Themes**. The build fails if a theme has the name of one of
Keycloak's own themes (`base`, `keycloak`, `keycloak.v2`).

## Providers

Put provider jars, such as custom authenticators, user storage, event
listeners or protocol mappers, in `providers/`. Build them for the Keycloak
version you run.

## Files

| Path | Purpose |
| --- | --- |
| `themes/` | Your Keycloak themes |
| `providers/` | Your provider jars |
| `.wodby/pipeline.yml` | The Wodby CI pipeline that builds and deploys the image |
| `.dockerignore` | Files left out of the build |
