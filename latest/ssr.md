# SSR (additional components)

## Using [Next.js](https://nextjs.org/) 13 with _app directory_?

Then check out [this article](https://locize.com/blog/next-13-app-dir-i18n) describing how to best internationalize it with i18next.

[![](../.gitbook/assets/next-13-app-dir-i18n.jpg)](https://locize.com/blog/next-13-app-dir-i18n)

## Using [Next.js](https://nextjs.org/)?

You should have a look at [next-i18next](https://github.com/i18next/next-i18next) which extends react-i18next to bring it to next.js the easiest way.

> With `next-i18next@v8.0.0` and `Next.js v10`, next-i18next has done a major rewrite of the package, leveraging the built-in [internationalized routing](https://nextjs.org/docs/advanced-features/i18n-routing) provided by Next.js.
>
> [Here](https://github.com/locize/next-i18next-locize) you can also find a next-i18next app example in combination with locize, that offers 2 different approaches.
>
> `next-i18next@v5.0.0` supports `Next.js v9.5` in [**Serverless** mode](https://nextjs.org/blog/next-8#serverless-nextjs) (as of [July 2020](https://github.com/isaachinman/next-i18next/issues/274#issuecomment-664616304)). If your goal is to use earlier versions of Next.js with Serverless, then you should have a look at ["Next Right Now"](https://github.com/UnlyEd/next-right-now), which is a Next.js 9 boilerplate with built-in `i18next`, `react-i18next` and Locize.
>
> **Looking for an optimized Next.js translations setup?**\
> [Here](https://locize.com/blog/next-i18next/) you'll find a blog post on how to best use next-i18next with client side translation download and SEO optimization.
>
> [![](../.gitbook/assets/next-i18next.jpg)](https://locize.com/blog/next-i18next/)
>
>
>
> **Using SSG / `next export`?**\
> [Here](https://locize.com/blog/next-i18n-static/) you'll find a simple tutorial on how to best use next-i18next in a SSG environment.\
> [<img src="../.gitbook/assets/next-ssg.jpeg" alt="" data-size="original">](https://locize.com/blog/next-i18n-static/)

## Using [Remix](https://remix.run)?

You should have a look at [remix-i18next](https://github.com/sergiodxa/remix-i18next) which extends react-i18next to bring it to Remix the easiest way.

> [Here](https://github.com/locize/locize-remix-i18next-example) you'll find a simple example and [here a step by step tutorial](https://locize.com/blog/remix-i18n/) on how to best use remix-i18next.
>
> [![](../.gitbook/assets/remix-localization.jpg)](https://locize.com/blog/remix-i18n/)

## Using [Gatsby](https://www.gatsbyjs.com/)?

You should have a look at [gatsby-plugin-react-i18next](https://github.com/microapps/gatsby-plugin-react-i18next) which extends react-i18next to bring it to Gatsby the easiest way.

> [Here](https://github.com/locize/locize-gatsby-example) you'll find a simple example and [here a step by step tutorial](https://locize.com/blog/gatsby-i18n/) on how to best use [gatsby-plugin-react-i18next](https://github.com/microapps/gatsby-plugin-react-i18next).
>
> [![](../.gitbook/assets/gatsby-i18next.jpg)](https://locize.com/blog/gatsby-i18n/)

## Setting the i18next instance based on req

Use the [I18nextProvider](i18nextprovider.md) to inject the i18next instance for example bound to the http i18n instance on the request object using [i18next-http-middleware](https://github.com/i18next/i18next-http-middleware).

```jsx
<I18nextProvider i18n={req.i18n}>
  <App />
</I18nextProvider>
```

## Passing initial translations / initial language down to client

To avoid asynchronous loading of translation on the client side (and the possible Suspense out of that) you will need to pass down initialLanguage (will call changeLanguage on i18next) and initialI18nStore (will prefill translations in i18next store).

### using the useSSR hook

```jsx
import React from 'react';
import { useSSR } from 'react-i18next';

export function InitSSR({ initialI18nStore, initialLanguage }) {
  useSSR(initialI18nStore, initialLanguage);

  return <App />
}
```

### using the withSSR HOC

```jsx
import React from 'react';
import { withSSR } from 'react-i18next';
import App from './App';

const ExtendedApp = withSSR()(App);

<ExtendedApp initialLanguage={} initialI18nStore={} />
```

The ExtendedApp in this case will also have the composed `ExtendedApp.getInitialProps()`
