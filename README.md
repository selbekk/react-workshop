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

Ready? Let's start!

------

## Compound components

Compound components are several components that work together to create a united
experience. A great example from the HTML world is `<select>` and `<option>` 
tags - one without the other doesn't do much, but together, they rule the world 
(or, well, let's you pick a value from a list of values). 

We're going to start this workshop off by using React's `cloneElement` API to 
inject props into our children.

### Example

### Tasks

#### Pass a property to a child

[Do your work here]()

#### Propagate a property to all children

[Do your work here]()

#### Create an input group component (ID + aria-invalid)

[Do your work here]()

#### Re-create a select-box with only DIVs

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

### Tasks

#### Create a simple HOC (hasProps)

[Do your work here]()

#### `withToggler`

[Do your work here]()

#### `withScreenSize`

[Do your work here]()

#### `withConnectivity`

[Do your work here]()

#### `withSpinner`

[Do your work here]()

#### `withDebugLogging`

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
