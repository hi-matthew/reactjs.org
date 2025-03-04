---
title: 'React v15.0 Release Candidate 2'
layout: Post
author: [zpao]
---

Today we're releasing a second release candidate for version 15. Primarily this is to address 2 issues, but we also picked up a few small changes from new contributors, including some improvements to some of our new warnings.

The most pressing change that was made is to fix a bug in our new code that removes `<span>`s, as discussed in the original RC1 post. Specifically we have some code that takes a different path in IE11 and Edge due to the speed of some DOM operations. There was a bug in this code which didn't break out of the optimization for `DocumentFragment`s, resulting in text not appearing at all. Thanks to the several people who [reported this](https://github.com/facebook/react/issues/6246).

The other change is to our SVG code. In RC1 we had made the decision to pass through all attributes directly. This led to [some confusion with `class` vs `className`](https://github.com/facebook/react/issues/6211) and ultimately led us to reconsider our position on the approach. Passing through all attributes meant that we would have two different patterns for using React where things like hyphenated attributes would work for SVG but not HTML. In the future, we _might_ change our approach to the problem for HTML as well but in the meantime, maintaining consistency is important. So we reverted the changes that allowed the attributes to be passed through and instead expanded the SVG property list to include all attributes that are in the spec. We believe we have everything now but definitely [let us know](https://github.com/facebook/react/issues/1657#issuecomment-197031403) if we missed anything. It was and still is our intent to support the full range of SVG tags and attributes in this release.

Thanks again to everybody who has tried the RC1 and reported issues. It has been extremely important and we wouldn't be able to do this without your help!

## Installation {#installation}

We recommend using React from `npm` and using a tool like browserify or webpack to build your code into a single bundle. To install the two packages:

- `npm install --save react@15.0.0-rc.2 react-dom@15.0.0-rc.2`

Remember that by default, React runs extra checks and provides helpful warnings in development mode. When deploying your app, set the `NODE_ENV` environment variable to `production` to use the production build of React which does not include the development warnings and runs significantly faster.

If you can’t use `npm` yet, we provide pre-built browser builds for your convenience, which are also available in the `react` package on bower.

- **React**  
  Dev build with warnings: <https://fb.me/react-15.0.0-rc.2.js>  
  Minified build for production: <https://fb.me/react-15.0.0-rc.2.min.js>
- **React with Add-Ons**  
  Dev build with warnings: <https://fb.me/react-with-addons-15.0.0-rc.2.js>  
  Minified build for production: <https://fb.me/react-with-addons-15.0.0-rc.2.min.js>
- **React DOM** (include React in the page before React DOM)  
  Dev build with warnings: <https://fb.me/react-dom-15.0.0-rc.2.js>  
  Minified build for production: <https://fb.me/react-dom-15.0.0-rc.2.min.js>
