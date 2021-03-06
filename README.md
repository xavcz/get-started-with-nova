> **Disclaimer:** I cannot ensure you'll be able to make this package work :) If you have any question, don't hesitate to drop by Slack: http://slack.telescopeapp.org


# Build with Nova

### What's up?
Experiment stuff on a custom package with Nova: `react-storybook` & `styled-components`

### NPM Dependencies
```sh
getstorybook

npm install --save styled-components@1.3.1 # this version is compatible with Nova's SSR `postRender` hook
```

### `.meteor/packages`

```
############ Core Packages ############

nova:core                       # core components and wrappers
nova:forms                      # auto-generated forms
nova:routing                    # routing and server-side rendering
nova:email                      # email
nova:users                      # user management and permissions

############ Features Packages ############

nova:posts
nova:categories
nova:events
nova:embedly

nova:i18n-en-us

accounts-twitter

build-with-nova
```

### `.storybook/config.js`
```js
import React from 'react';
import { configure, addDecorator } from '@kadira/storybook';

import '../packages/build-with-nova/styles.css';
import { Wrapper } from '../packages/build-with-nova/lib/components/Layout';

const LayoutDecorator = story =>
  <Wrapper>{story()}</Wrapper>

addDecorator(LayoutDecorator);

const req = require.context(
  '../packages/build-with-nova/lib/components', 
  true, 
  /.stories.js$/
);

function loadStories() {
  req.keys().forEach((filename) => req(filename))
}

configure(loadStories, module);
```

Happy hacking 🚀 🔭
