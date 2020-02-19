# Lighthouse for Azure Pipelines

This is an Azure DevOps extension that allows you to **enhance your Azure Pipelines with a Lighthouse tab**.
The Lighthouse tab embed one or many HTML reports generated by [Google Lighthouse](https://developers.google.com/web/tools/lighthouse/).

The task only requires a target URL to execute Lighthouse against.

If the [Lighthouse NPM package](https://www.npmjs.com/package/lighthouse) is already installed locally or globally on the agent, then the task will use it.
Otherwise, it will install the latest version in a temporary folder.

![Lighthouse HTML report embed in a tab](https://raw.githubusercontent.com/gsoft-inc/azure-pipelines-lighthouse/master/docs/lh-result.png)

You can also specify **audit score assertions** that can make the pipeline fail based on the audit scores.

For example, the Google Lighthouse audit `no-vulnerable-libraries` produces a boolean score that will be equal to 1 if there are no known vulnerabilities within client-side JavaScript libraries and frameworks detected on a web site.
This is an example of a score assertion for this audit:

```
no-vulnerable-libraries = 1
```

Which means that you expect the audit `no-vulnerable-libraries` to have a score equal to `1`.

**Any audit score generated by Lighthouse is between 0 and 1**. You can also use the `>` (greater than) and the `<` (lower than) operator to evaluate decimal audit scores.
Audit score assertions must be written on separate lines.

![Lighthouse task](https://raw.githubusercontent.com/gsoft-inc/azure-pipelines-lighthouse/master/docs/lh-task.png)

## Installation

Lighthouse for Azure Pipelines can be installed from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=GSoft.lighthouse-vsts).

## Available audits

The following audits exist in Lighthouse 5.6.0. More may be added in the future.

| Audit                              | Type    | Description                                                                                                                        |
| ---------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| is-on-https                        | binary  | Uses HTTPS                                                                                                                         |
| redirects-http                     | binary  | Redirects HTTP traffic to HTTPS                                                                                                    |
| service-worker                     | binary  | Does not register a service worker that controls page and `start_url`                                                              |
| works-offline                      | binary  | Current page does not respond with a 200 when offline                                                                              |
| viewport                           | binary  | Has a `<meta name="viewport">` tag with `width` or `initial-scale`                                                                 |
| without-javascript                 | binary  | Contains some content when JavaScript is not available                                                                             |
| first-contentful-paint             | numeric | First Contentful Paint                                                                                                             |
| first-meaningful-paint             | numeric | First Meaningful Paint                                                                                                             |
| load-fast-enough-for-pwa           | binary  | Page load is fast enough on mobile networks                                                                                        |
| speed-index                        | numeric | Speed Index                                                                                                                        |
| estimated-input-latency            | numeric | Estimated Input Latency                                                                                                            |
| total-blocking-time                | numeric | Total Blocking Time                                                                                                                |
| max-potential-fid                  | numeric | Max Potential First Input Delay                                                                                                    |
| errors-in-console                  | binary  | No browser errors logged to the console                                                                                            |
| time-to-first-byte                 | binary  | Server response times are low (TTFB)                                                                                               |
| first-cpu-idle                     | numeric | First CPU Idle                                                                                                                     |
| interactive                        | numeric | Time to Interactive                                                                                                                |
| redirects                          | numeric | Avoid multiple page redirects                                                                                                      |
| installable-manifest               | binary  | Web app manifest does not meet the installability requirements                                                                     |
| apple-touch-icon                   | binary  | Does not provide a valid `apple-touch-icon`                                                                                        |
| splash-screen                      | binary  | Is not configured for a custom splash screen                                                                                       |
| themed-omnibox                     | binary  | Does not set a theme color for the address bar.                                                                                    |
| content-width                      | binary  | Content is sized correctly for the viewport                                                                                        |
| image-aspect-ratio                 | binary  | Displays images with correct aspect ratio                                                                                          |
| deprecations                       | binary  | Avoids deprecated APIs                                                                                                             |
| mainthread-work-breakdown          | numeric | Minimize main-thread work                                                                                                          |
| bootup-time                        | numeric | Reduce JavaScript execution time                                                                                                   |
| uses-rel-preload                   | numeric | Preload key requests                                                                                                               |
| uses-rel-preconnect                | numeric | Preconnect to required origins                                                                                                     |
| font-display                       | binary  | All text remains visible during webfont loads                                                                                      |
| offline-start-url                  | binary  | `start_url` does not respond with a 200 when offline                                                                               |
| third-party-summary                | binary  | Reduce the impact of third-party code                                                                                              |
| aria-allowed-attr                  | binary  | `[aria-*]` attributes match their roles                                                                                            |
| aria-required-attr                 | binary  | `[role]`s do not have all required `[aria-*]` attributes                                                                           |
| aria-required-children             | binary  | Elements with an ARIA `[role]` that require children to contain a specific `[role]` have all required children.                    |
| aria-required-parent               | binary  | `[role]`s are contained by their required parent element                                                                           |
| aria-roles                         | binary  | `[role]` values are valid                                                                                                          |
| aria-valid-attr-value              | binary  | `[aria-*]` attributes have valid values                                                                                            |
| aria-valid-attr                    | binary  | `[aria-*]` attributes are valid and not misspelled                                                                                 |
| button-name                        | binary  | Buttons have an accessible name                                                                                                    |
| bypass                             | binary  | The page does not contain a heading, skip link, or landmark region                                                                 |
| color-contrast                     | binary  | Background and foreground colors do not have a sufficient contrast ratio.                                                          |
| document-title                     | binary  | Document has a `<title>` element                                                                                                   |
| duplicate-id                       | binary  | `[id]` attributes on the page are unique                                                                                           |
| html-has-lang                      | binary  | `<html>` element has a `[lang]` attribute                                                                                          |
| html-lang-valid                    | binary  | `<html>` element has a valid value for its `[lang]` attribute                                                                      |
| image-alt                          | binary  | Image elements have `[alt]` attributes                                                                                             |
| label                              | binary  | Form elements have associated labels                                                                                               |
| link-name                          | binary  | Links do not have a discernible name                                                                                               |
| meta-viewport                      | binary  | `[user-scalable="no"]` is not used in the `<meta name="viewport">` element and the `[maximum-scale]` attribute is not less than 5. |
| tabindex                           | binary  | No element has a `[tabindex]` value greater than 0                                                                                 |
| uses-long-cache-ttl                | numeric | Uses efficient cache policy on static assets                                                                                       |
| total-byte-weight                  | numeric | Avoids enormous network payloads                                                                                                   |
| offscreen-images                   | numeric | Defer offscreen images                                                                                                             |
| render-blocking-resources          | numeric | Eliminate render-blocking resources                                                                                                |
| unminified-css                     | numeric | Minify CSS                                                                                                                         |
| unminified-javascript              | numeric | Minify JavaScript                                                                                                                  |
| unused-css-rules                   | numeric | Remove unused CSS                                                                                                                  |
| uses-webp-images                   | numeric | Serve images in next-gen formats                                                                                                   |
| uses-optimized-images              | numeric | Efficiently encode images                                                                                                          |
| uses-text-compression              | numeric | Enable text compression                                                                                                            |
| uses-responsive-images             | numeric | Properly size images                                                                                                               |
| efficient-animated-content         | numeric | Use video formats for animated content                                                                                             |
| appcache-manifest                  | binary  | Avoids Application Cache                                                                                                           |
| doctype                            | binary  | Page has the HTML doctype                                                                                                          |
| dom-size                           | numeric | Avoids an excessive DOM size                                                                                                       |
| external-anchors-use-rel-noopener  | binary  | Links to cross-origin destinations are safe                                                                                        |
| geolocation-on-start               | binary  | Avoids requesting the geolocation permission on page load                                                                          |
| no-document-write                  | binary  | Avoids `document.write()`                                                                                                          |
| no-vulnerable-libraries            | binary  | Avoids front-end JavaScript libraries with known security vulnerabilities                                                          |
| js-libraries                       | binary  | Detected JavaScript libraries                                                                                                      |
| notification-on-start              | binary  | Avoids requesting the notification permission on page load                                                                         |
| password-inputs-can-be-pasted-into | binary  | Allows users to paste into password fields                                                                                         |
| uses-http2                         | binary  | Uses HTTP/2 for its own resources                                                                                                  |
| uses-passive-event-listeners       | binary  | Does not use passive listeners to improve scrolling performance                                                                    |
| meta-description                   | binary  | Document does not have a meta description                                                                                          |
| http-status-code                   | binary  | Page has successful HTTP status code                                                                                               |
| font-size                          | binary  | Document uses legible font sizes                                                                                                   |
| link-text                          | binary  | Links have descriptive text                                                                                                        |
| is-crawlable                       | binary  | Page isn’t blocked from indexing                                                                                                   |
| robots-txt                         | binary  | robots.txt is valid                                                                                                                |
| tap-targets                        | binary  | Tap targets are not sized appropriately                                                                                            |
| hreflang                           | binary  | Document has a valid `hreflang`                                                                                                    |
| plugins                            | binary  | Document avoids plugins                                                                                                            |

## Compiling

There are GitHub actions that take care of compiling, packaging and publishing the extension.

## License

Copyright © 2020, Groupe GSoft Inc. This code is licensed under the Apache License, Version 2.0. You may obtain a copy of this license at https://github.com/gsoft-inc/azure-pipelines-lighthouse/blob/master/LICENSE.
