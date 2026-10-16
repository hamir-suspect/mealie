# Contributing with Translations
Translations can be a great way **for non-coders** to contribute to project.
We use **[Crowdin](https://crowdin.com/project/mealie)** to allow several contributors to work on translating Mealie.
You can simply help by voting for your preferred translations, or even by completely translating Mealie into a new language.

Translations are regularly pulled from Crowdin and included in each new release.

Please use Crowdin as much as possible if you have any question/issue regarding a particular string. You can take a look at [Crowdin Knowledge base](https://support.crowdin.com/for-volunteer-translators/) if you want to know more about how to use this tool.

## My language is missing in Mealie
Once your language is translated on Crowdin, we need to manually add it in Mealie. If you believe your language is ready for use, please create an issue on GitHub.

## I can't find a particular text in Crowdin
There can be several reasons:
- The text you're looking for is outdated: someone has already changed it or it will be removed/changed in the next release.
- It is possible some texts are not translatable (yet) for technical reasons. If you spot one, please reach out to us on [Discord](https://discord.gg/QuStdQGSGK) or raise an issue on GitHub.

## Croatian release maintained in this fork

This fork maintains a complete Croatian catalog for Mealie v3.28.0. It is
independent of Crowdin's upstream approval and translation-progress metrics.
Upstream contributions must still follow the Crowdin workflow above.

The Croatian UI messages, backend messages, food seed data, and unit seed
data are maintained together. Interpolation parameters, Markdown links,
technical identifiers, and intentionally empty source fields are preserved.
Recipe content and existing database records are not translated or reseeded.
The interface language remains a browser preference, not an account setting.

Build the translation-only image from the release branch:

```sh
docker build -f docker/Dockerfile.croatian \
  --build-arg SOURCE_REVISION="$(git rev-parse HEAD)" \
  -t mealie:3.28.0-hr.1 .
```

This rebuilds the v3.28.0 frontend and layers it and the Croatian package
resources onto the official v3.28.0 image. No backend dependency upgrade or
database migration is included. Keep a consistent backup of `/app/data`
before deployment, retain the original image for rollback, and recreate the
container using the same data volume.

After deployment, choose **Settings → Language → Hrvatski (Croatian)**.
Browsers with an existing service worker may need a reload to pick up the
new frontend assets. Verify recipe reading, cookbook navigation, shopping
lists, import messages, plural forms, and that another browser can remain
in English.
