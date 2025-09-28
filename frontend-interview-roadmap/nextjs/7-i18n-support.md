
# 7. Internationalization (i18n) Support in Next.js

## Quick Revision

**Internationalization (i18n)** is the process of designing and developing an application in a way that makes it adaptable to different languages and regions without engineering changes. Next.js provides built-in support for i18n, allowing you to easily configure locales, detect user language, and manage translations.

## Detailed Explanation

Next.js offers a robust solution for internationalization, which is crucial for applications targeting a global audience. It allows you to define different locales (languages and regions) and automatically handles routing and serving the correct content based on the user's preferred language.

### How Next.js i18n Works

1.  **Configuration:** You define your supported locales in `next.config.js`.

    ```javascript
    // next.config.js
    module.exports = {
      i18n: {
        locales: ['en', 'fr', 'ar'],
        defaultLocale: 'en',
        localeDetection: false, // Optional: disable automatic locale detection
      },
    };
    ```

2.  **Routing:** Next.js automatically handles routing for different locales. For example, if you have a page `pages/about.js` and locales `en` and `fr`, Next.js will create routes like `/en/about` and `/fr/about`.

3.  **Locale Detection:** By default, Next.js tries to detect the user's preferred locale from the `Accept-Language` header. You can disable this with `localeDetection: false`.

4.  **Accessing Locale Information:** You can access the current locale using the `useRouter` hook or `context.locale` in data fetching functions.

### Managing Translations

Next.js itself doesn't provide a built-in translation management system. You typically integrate with a third-party library for this, such as `next-i18next` or `react-i18next`.

**`next-i18next`** is a popular choice as it integrates `react-i18next` with Next.js, providing server-side rendering support for translations.

## Code Examples

### `next.config.js` Configuration

```javascript
// next.config.js
module.exports = {
  i18n: {
    locales: ['en-US', 'fr-FR', 'ar-AE'],
    defaultLocale: 'en-US',
    domains: [
      {
        domain: 'example.com',
        defaultLocale: 'en-US',
      },
      {
        domain: 'example.fr',
        defaultLocale: 'fr-FR',
        // An optional array of locale prefixes that this domain supports.
        // If a locale is not specified, then the defaultLocale value will be used.
        locales: ['fr-FR'],
      },
    ],
  },
};
```

### Accessing Locale in a Page

```jsx
import { useRouter } from 'next/router';

function HomePage() {
  const router = useRouter();
  const { locale, locales, defaultLocale } = router;

  return (
    <div>
      <h1>Current Locale: {locale}</h1>
      <p>Supported Locales: {locales.join(', ')}</p>
      <p>Default Locale: {defaultLocale}</p>

      <a href="/fr">Switch to French</a>
    </div>
  );
}

export default HomePage;
```

### Using `next-i18next` (Conceptual)

```jsx
// pages/index.js
import { useTranslation } from 'next-i18next';
import { serverSideTranslations } from 'next-i18next/serverSideTranslations';

function HomePage() {
  const { t } = useTranslation('common');

  return (
    <div>
      <h1>{t('welcome')}</h1>
      <p>{t('description')}</p>
    </div>
  );
}

export async function getStaticProps({ locale }) {
  return {
    props: {
      ...(await serverSideTranslations(locale, ['common'])),
    },
  };
}

export default HomePage;
```

## Resources

*   **Article:** [Next.js Docs - Internationalized Routing](https://nextjs.org/docs/advanced-features/i18n-routing)
*   **Library:** [next-i18next](https://github.com/i18next/next-i18next)
*   **Video:** [Next.js i18n Tutorial - Traversy Media](https://www.youtube.com/watch?v=K7C_0_2_200)
