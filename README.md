### Hyperapp#2 Middlewares

Hyperapp#2 provides awesome middleware mechanics based on wrapping internal dispatch function, those allows creation of custom dispatch behavior and multiple useful helpers (middlewares). This package is a set of frequently used middlewares.

### Install
This package is not published to npm registry yet,
to install use github repository path as package name
```bash
npm install sergey-shpak/hyperapp-middlewares
```

#### List of middlewares

##### onState
Triggers callback when state object has been dispatched
```javascript
import { app } from 'hyperapp'
import { onState } from '@hyperapp/middlewares'

app({
  // ... app initialization
  middleware: onState(state => console.log("State", state))
})
```

##### onAction (onTuple)
Triggers callback when action/tuple has been dispatched
```javascript
import { app } from 'hyperapp'
import { onAction } from '@hyperapp/middlewares'

app({
  // ... app initialization
  middleware: onAction(action => console.log("Action", action))
})
```

##### onEffect
Triggers callback when effect has been dispatched
```javascript
import { app } from 'hyperapp'
import { onEffect } from '@hyperapp/middlewares'

app({
  // ... app initialization
  middleware: onEffect(effect => console.log("Effect", effect))
})
```

##### Middlewares action/props propagation
For 'onState', 'onAction', 'onTuple' and 'onEffect' return new value from middleware callback to override propagated action, like
```javascript
  middleware: onState(state => ({ prop: 'new state' }))
```

##### logger
Logs each dispatched action. Takes two arguments:
- custom `output` function ('console.debug' by default)
- and `verbose` option to log 'tuples' and 'effects'

```javascript
import { app } from 'hyperapp'
import { logger } from '@hyperapp/middlewares'

app({
  // ... app initialization settings
  // log only when running in 'development' env
  middleware: process.env.NODE_ENV === 'development' && logger()
})
```

or with custom output and verbose option
```javascript
import { app } from 'hyperapp'
import { logger } from '@hyperapp/middlewares'

// custom logger output
const output = (...logs) => {}

app({
  // ... app initialization settings
  middleware: logger(output, true)
})
```

##### immutable
Makes state object immutable, all state mutations fails.
(When running in 'strict mode' environment, error is thrown on any state mutation, action triggered mutation is visible through error stack trace).
```javascript
import { app } from 'hyperapp'
import { immutable } from '@hyperapp/middlewares'

app({
  // ... app initialization settings
  middleware: immutable
})
```

##### compose
Creates middlewares composition
```javascript
import { app } from 'hyperapp'
import { logger, immutable, compose } from '@hyperapp/middlewares'

app({
  // ... app initialization settings
  // compose(middleware, .., middlewareN)
  middleware: compose(immutable, logger())
})
```

### License
@hyperapp/middlewares is MIT licensed. See [LICENSE](LICENSE.md).
