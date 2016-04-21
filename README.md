# SystemJS hot reloader store
Extremely simple utility for storing data across hot reloads.  
Compatible with: [systemjs-hot-reloader](https://github.com/capaj/systemjs-hot-reloader).  
This works because the data is put in a seperate module that isn't reloaded. See: https://github.com/capaj/systemjs-hot-reloader#preserving-state

## Install
```
jspm install systemjs-hot-reloader-store
```

## Usage
``` javascript
import getHotReloadStore from './utils/getHotReloadStore.js';
const hotStore = getHotReloadStore('project:index'); // pick unique name

// retrieve stored or create new state
const state = hotStore.state || {
	counter: 0
};

// change state
state.counter += 1;

// store state
hotStore.state = state;
```

## Redux example
``` javascript
import { createStore } from 'redux';
import getHotReloadStore from './utils/getHotReloadStore.js';
const hotStore = getHotReloadStore('project:store');

let prevState;
if (hotStore.prevStore) {
  prevState = hotStore.prevStore.getState(); 
}

export default function configureStore(reducers, initialState = prevState) {
  const store = createStore(reducers, initialState); 
  hotStore.prevStore = store;
  return store;
}
```
