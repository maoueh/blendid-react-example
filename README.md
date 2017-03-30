# Blendid - React

This repository show a small example of using React library with Blendid. It
just the bare minimum setup and I did not test every React feature (yet).

I have a real project that I want to integrate Blendid in, but for now, here
the minimal steps.

## Steps

Here the list of steps used to create this repository.

### Initial setup

```
mkdir /tmp/blendid-react-example
cd /tmp/blendid-react-example

git init .

yarn init
yarn add --dev blendid
yarn run blendid -- init
```

### Initial commit

Make an initial commit so it's easy to see React specific changes.

```
echo 'node_modules/' > .gitignore

git add -A .
git commit -m "Initial commit"
```

### React

This is where React specific stuff are added.

```
yarn add react react-dom
yarn add --dev babel-preset-react-app
```

Then, let's configure Blendid Babel to use React preset by opening the file
`config/task-config.js` and adding presets to the `javascripts` config block:

```
babel: {
  presets: ['react-app']
}
```

So the blocks look like:

```
javascripts: {
  entries: {
    app: ["./app.js"]
  },
  extensions: ["js", "json"],
  extractSharedJs: false,
  babel: {
    presets: ['react-app']
  }
},
```

Update `src/html/index.html` so that block content now looks like:

```
{% block content %}
  <div id='root'></div>
{% endblock %}
```

And finally edit `src/javascripts/app.js` so it looks like:

```
import './modules'

import React from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```

### Run

Last thing is to actually run the sample project with React integrated. For now,
you will need to set the `BABEL_ENV` manually but will send a PR to Blendid
repo to make it automatic:

```
BABEL_ENV=development yarn run blendid
```

Voila!
