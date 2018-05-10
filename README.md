# Advanced React Patterns tutorial

This is the tasks and assignments for the Advanced React Patterns tutorial, held
by @selbekk et al.

You can find the slides associated to this workshop somewhere online once I've
made them.

## About this workshop

This workshop aims to introduce some advanced patterns and techniques for 
passing properties and sharing logic across your application. We'll start off 
with some pretty basic stuff, and continue on working through a slew of tasks on 
each topic. It's totally fine if you don't finish all the tasks - we created 
several  extras so that you can continue your learning on your own at your own 
pace.

### Intended audience

This workshop assumes that you know the basics of React, and that you're pretty 
comfortable writing your own components. If you want to brush up on your React 
skills before attending this workshop, I suggest you look through the 
[Beginner's guide to React](https://egghead.io/courses/the-beginner-s-guide-to-react)
by Kent C. Dodds. Don't be put off by the title - even React pros can learn a 
trick or two from watching this 80 minutes of video.

------

## Compound components

Compound components are several components that work together to create a united
experience. A great example from the HTML world is `<select>` and `<option>` 
tags - one without the other doesn't do much, but together, they rule the world 
(or, well, let's you pick a value from a list of values). 

We're going to start this workshop off by using React's `cloneElement` API to 
inject props into our children.

### Example

[`React.cloneElement`](https://reactjs.org/docs/react-api.html#cloneelement) is 
a way to, well, clone a React element. We typically use it to apply extra props
to the children passed to our component. Here's an example of how it's used:

```js
const RadioButtonGroup = (props) => (
  <div>
    {React.Children.map(
      props.children, 
      (child) => React.cloneElement(child, { name: props.name }),
    )}
  </div>
);
```

Here, we loop over all the children (`React.Children.map`), and pass the `name` 
prop from `RadioButtonGroup` to each child. This way, we don't have to pass this 
prop to each child manually!

```js
<RadioButtonGroup name="choice">
  <input type="radio" value="red" />
  <input type="radio" value="blue" />
  <input type="radio" value="green" />
</RadioButtonGroup>
```

### Tasks

Do as many of these as you get to before the time is out. You're not supposed to 
finish them all as a part of the workshop.

#### Pass another property to the children

Continuing the `RadioButtonGroup` example from earlier - we notice that the 
`type="radio"` prop is everywhere as well! Change the example code to pass this 
prop directly to all children as well.

[Do your work here]()

#### Make all the elements red!

Just for funs, create a component that applies a red border to all its children.
It's probably useful for debugging at some point. I guess.

[Do your work here]()

#### Who's going to win?

What happens when you pass in children that already have a prop with the same 
name as you're trying to overwrite? Let's find out!

Create a component that applies a class of "clone-element-class" to its 
children. Also make sure to pass in children with the "original-class" class.
Which one wins? Can you make a component that lets you apply the 
`clone-element-class` _and_ the `original-class` class to the children?

[Do your work here]()

#### Create an input group component (ID + aria-invalid)

Another similar component to the `RadioButtonGroup` could be a component that 
lets you add a label and an error message to your component. We've created the 
outline to such a component in the sandbox below. 

To make sure our component is accessible, the child needs a unique ID and an 
aria-tag indicating whether or not it's invalid. Propagate two props - a unique
`id` string and `aria-invalid`, which should be either `"true"` or `"false"` 
depending on whether the `error` prop is set or not.

[Do your work here]()

(Tip: You _can_ use `uuid` for generating unique IDs)

#### Re-create a select-box with only DIVs

As we mentioned in the beginning of this section, the `<select>` and `<option>` 
tags are great examples of how a compound component could work. Let's try to 
recreate that!

Create a `<Select />` component and an `<Option />` component that try to 
replicate the original behavior as closely as possible. Use `React.cloneElement` 
to provide the `<Option />` tags with `onClick` handlers and all the goodies 
you need.

[Do your work here]()

### Summary

Using `cloneElement` is great for when you know you'll only have a single type 
of children, or if you just have really simple component structures.

When you need more flexibility or access to lifecycle methods, you might want 
to consider other options.

## Higher order components

Higher order components is a powerful pattern for when you need to access the 
lifecycle methods of React, or simply need to share logic across your 
application.

Higher order components (also known as HOCs) are functions that accept a 
component as input, and returns a new component that potentially renders your 
input with some extra props.

You've probably used HOCs before. `react-redux`' `connect` and `react-router`'s 
`withRouter` are both HOCs that wrap your component and gives it more 
information and capabilities than it did before.

### Example

Here's a simple HOC that provides your component with some hard coded user info:

```js
// First, let's create some fake user info.
const userInfo = { name: 'Kristofer', age: 30 };
const withUserInfo = (TargetComponent) => 
  props => <TargetComponent {...props} {...userInfo} />;
};
```

Here, we create a function that accepts a component, and then returns a _new_ 
component that renders the passed component with the extra `name` and `age` 
props.

You can use it like this:

```js
const Greeting = props => (
  <p>
    Hi {props.name}, you don't look a day over {props.age - 5}!
  </p>
);
const GreetingWithUserInfoAlreadyProvided = withUserInfo(Greeting);
```

### Tasks

#### `withColor`

Let's start off without too much frills. Create an HOC that adds the prop 
`color="yellow"` to the passed component. 

[Do your work here]()

#### `withToggler`

HOCs can return stateful class components as well. The sandbox below has a 
simple outline of a Toggle component implemented. Pass two props `toggled` and 
`onToggle` down to the wrapped component!

[Do your work here]()

#### `withScreenSize`

Sometimes, you don't want to render something big on small devices. Therefore, 
we need to create an HOC `withScreenSize` that provides two props `screenWidth`
and `screenHeight` to its wrapped component. 

Bonus task: Remember to update the props when the screen size changes!

[Do your work here]()

Tip: You get the screen size from `window.screen`.

Tip: Use a debounce function like 
[`lodash/debounce`](https://www.npmjs.com/package/lodash.debounce)

#### `withConnectivity`

Sometimes, you want to react to changes in connectivity. From no-fi to wi-fi to
mobile connections - showing different UIs might be something your app requires.
At least this workshop does.

Create an HOC that provides a `connectivity` prop with the current connection 
status.

[Do your work here]()

Tip: [Here's some info](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API) 
on how to get the connectivity status

#### `withSpinner`

We often fetch data. Why not create a component that renders a spinner for us 
when we're fetching data?

Create an HOC that renders a `<Spinner />` whenever the `loading`, `pending` or 
`fetching` props are true. If they are false - just return the passed component.

[Do your work here]()

#### `withDebugLogging`

Do you write a lot of `console.log` statements, even though there's a perfectly 
good debugger available? We too. Create an HOC that wraps your buggy component, 
that logs:

- whenever the wrapped component renders (with timestamp)
- whenever the props change (with the old and new props)

[Do your work here]()

### Summary

Higher order components are powerful tools that lets you do basically whatever 
you want - as long as you want to apply any extra props etc directly to your 
passed component.

If you don't know how your consumer wants to use the data you provide, you might
want to look at other alternatives.

## Render props

The concept of "render props" is one of the most powerful patterns in React. It 
lets you harness the powers of HOCs, while at the same time retain the freedom 
you apply that power wherever you want.

"Render props" is the act of returning the result of calling a prop in your 
component's `render` method. That prop could be called whatever you want - even 
`children`. Since the `children` prop is handled a bit differently in JSX than 
the rest, this lets you pass in a function as children to your component:

```js
<MyRenderPropComponent>
  {magicProps => (
    <div>{magicProps.someData}</div>
  )}
</MyRenderPropComponent>
```

Woah!

### Example

### Tasks

#### My first render prop

[Do your work here]()

#### Function as child

[Do your work here]()

#### Re-implement the input group with render props

[Do your work here]()

#### Re-implement the toggle container with render props

[Do your work here]()

### Summary

Render props are powerful, and lets you share logic across your application with 
ease. They aren't always required, though, and the syntax can be a bit verbose. 
The moral of the story is "use when required".

## Context

Passing logic between components is now a breeze - right? Well, you almost know
all of the secrets! There's one more challenge to conquer though - and that's 
React's `context` API.

Every so often, you end up passing props from one component several layers down 
without using it at all. This is what we refer to as "prop drilling", and is a 
pain a lot of React developers deal with.

Context is a workaround for this. It lets you pass any value from any top 
component to any component further down the component tree without passing it 
through the intermediate "layers". 

Like HOCs, you've probably used context before - although not directly. The way 
you get access to the Redux store, or React Router's `history` object and route 
information, is through context. You use an HOC or a component to access the 
context, so you typically don't notice it at all!

### Example

#### Tasks

##### Creating context

[Do your work here]()

##### Providing context

[Do your work here]()

##### Consuming context

[Do your work here]()

##### Theme

[Do your work here]()

##### Internationalization

[Do your work here]()

##### "Redux"

[Do your work here]()

### Summary

Context works as a "wormhole" for props, letting you pass props from the top of 
the tree to any place below it without passing it through intermediary 
components. It's great when you work with deep component trees, or if you have 
application global state or content that you need to provide to your components.

Context also comes with the downside of a slightly verbose API. Sometimes it's 
just easier and more readable to just pass the prop a level or two. That's up to 
you - the developer - to decide

## Further reading

If you found these topics interesting, and want to learn more, there are some 
resources you can look into to further continue your learning.

- [Kent C. Dodds' course on advanced React](https://blog.kentcdodds.com/advanced-react-component-patterns-56af2b74bc5f)
- article on HOCs (the one I used for inspiration for tasks)
- article on render props
- the React docs
- article on context
- article on compound components

## Feedback!

The only way we get better is through feedback. Please provide us with some 
insights on how this workshop was perceived, what it excelled at, and where we
can improve.

[Feedback form is here]()

If you feel up for adding more tasks, fixing our spelling or whatever, please
let us know!
