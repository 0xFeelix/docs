---
title: Using TypeScript with React
type: article
sidebar: auto
---

# Using TypeScript with React
---

::: tip
While this tutorial has content that we believe is of great benefit to our community, we have not yet tested or edited it to ensure you have an error-free learning experience. It's on our list, and we're working on it! You can help us out by using the "report an issue" button at the bottom of the tutorial.
:::


TypeScript is awesome. So is React. Let’s use them both together! Using TypeScript allows us to get the benefits of IntelliSense, as well as the ability to further reason about our code. As well as this, adopting TypeScript is low-friction, as files can be incrementally upgraded without causing issues throughout the rest of your project.

Let’s start off by creating a new React project and integrate TypeScript. Run the following commands to initiate the project:

``` sh
# Make a new directory
$ mkdir react-typescript

# Change to this directory within the terminal
$ cd react-typescript

# Initialise a new npm project with defaults
$ npm init -y

# Install React dependencies
$ npm install react react-dom

# Make index.html and App.tsx in src folder
$ mkdir src
$ cd src
$ touch index.html
$ touch App.tsx

# Open the directory in your favorite editor
$ code .
```

We can then make an `index.html` file with the following:

``` html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>React + TypeScript</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
  <div id="main"></div>
  <script src="./App.tsx"></script>
</body>
</html>
```

We’ll be using Parcel as our bundler, but you can elect to use webpack or another bundler if you wish. Or, check this section if you prefer using Create React App. Let’s add Parcel to our project:

``` sh
# Install Parcel to our DevDependencies
$ npm i parcel-bundler -D

# Install TypeScript
$ npm i typescript -D

# Install types for React and ReactDOM
$ npm i -D @types/react @types/react-dom
```

We can update our `package.json` with a new task that will start our development server:

``` json
{
  "name": "react-typescript",
  "version": "1.0.0",
  "description": "An example of how to use React and TypeScript with Parcel",
  "scripts": {
    "dev": "parcel src/index.html"
  },
  "keywords": [],
  "author": "Paul Halliday",
  "license": "MIT"
}
```

We can now populate a `Counter.tsx` file with a simple counter:

``` jsx
import * as React from 'react';

export default class Counter extends React.Component {
  state = {
    count: 0
  };

  increment = () => {
    this.setState({
      count: (this.state.count + 1)
    });
  };

  decrement = () => {
    this.setState({
      count: (this.state.count - 1)
    });
  };

  render () {
    return (
      <div>
        <h1>{this.state.count}</h1>
        <button onClick={this.increment}>Increment</button>
        <button onClick={this.decrement}>Decrement</button>
      </div>
    );
  }
}
```

Then, inside of `App.tsx`, we can load the Counter:

``` jsx
import * as React from 'react';
import { render } from 'react-dom';

import Counter from './Counter';

render(<Counter />, document.getElementById('main'));
```

Our project can be ran with `$ npm run dev` and accessed at `http://localhost:1234`.



## Create React App and TypeScript

If you’d rather use Create React App to initiate your project, you’ll be pleased to know that CRA now supports TypeScript out of the box.

Just use the `--typescript` flag when invoking the `create-react-app` command:

``` sh
$ create-react-app my-new-app --typescript
```

## Functional Components

Stateless or functional components can be defined in TypeScript like so:

``` jsx 
import * as React from 'react';

const Count: React.FunctionComponent<{
  count: number;
}> = (props) => {
  return <h1>{props.count}</h1>;
};

export default Count;
```

We’re using `React.FunctionComponent` and defining the object structure of our expected props. In this scenario we’re expecting to be passed in a single prop named `count` and we’re defining it in-line. We can also define this in other ways, by creating an interface such as `Props`:

``` jsx 
interface Props {
  count: number;
}

const Count: React.FunctionComponent<Props> = (props) => {
  return <h1>{props.count}</h1>;
};
```


## Class Components

Class components can similarly be defined in TypeScript as such:

``` jsx 
import * as React from 'react';

import Count from './Count';

interface Props {}

interface State {
  count: number;
};

export default class Counter extends React.Component<Props, State> {
  state: State = {
    count: 0
  };

  increment = () => {
    this.setState({
      count: (this.state.count + 1)
    });
  };

  decrement = () => {
    this.setState({
      count: (this.state.count - 1)
    });
  };

  render () {
    return (
      <div>
        <Count count={this.state.count} />
        <button onClick={this.increment}>Increment</button>
        <button onClick={this.decrement}>Decrement</button>
      </div>
    );
  }
}
```

## Default Props

We can also define `defaultProps` in scenarios where we may want to set default props. We can update our Count example to show this:

```jsx
import * as React from 'react';

interface Props {
  count?: number;
}

export default class Count extends React.Component<Props> {
  static defaultProps: Props = {
    count: 10
  };

  render () {
    return <h1>{this.props.count}</h1>;
  }
} 
```

We’ll need to stop passing `this.state.count` in to the `Counter` component too, as this will overwrite our default prop:

```jsx
render () {
  return (
    <div>
      <Count />
      <button onClick={this.increment}>Increment</button>
      <button onClick={this.decrement}>Decrement</button>
    </div>
  )
}
```

You should now have a project that’s set up to use TypeScript and React, as well as the tools to create your own functional and class-based components!



---
[Back](/blog/)
