# Introduction to React
1. [JSX](#jsx)
2. [React Component](#react-component)
    - [Conventions](#conventions)
    - [State and Props](#state-and-props)
    - [Handling Events](#handling-events)
    - [Lifting State Up](#lifting-state-up)
    - [Lifecycle Methods](#lifecycle-methods)
3. [React Component Types](#react-component-types)
    - [Presentational and Container Components](#presentational-and-container-components)
    - [Class Component](#class-component)
    - [Functional Component](#functional-component)


## JSX
_Syntactic extensions to JavaScript which enables expressing react elements using HTML like syntax_
- Avoid separation of rendering logic from UI logic

```jsx
const element = (
  <h1 className="greeting">
    Hello World!
  </h1>
);
```
## React Component
_A component returns a set of React elements_
- Split UI into reusable and independent pieces
- Accept inputs

### Conventions
- User-defined component names must start with a capital letter
- Tags start with lowercase are treated as DOM tags (built-in components)

### State and Props
#### State
_Each component can store its own local information in its state_
- Can be passed as props to children
- Only class components can have local state
- Declared within the constructor
```javascript
constructor(props) {
  super(props);
  this.state = {
  }
}
```
- Should only be modified using `setState()`
```javascript
this.setState({
  selectedDish: dish
});
```
#### Props
_A parent component stores the state and the state information can be passed to the children in the use of props in the form of attributes_
- can pass in multiple attributes
```javascript
<Dishdetail dish={this.state.dish} comments={this.state.comments} />
```
### Handling Events
- use camelCase
- pass function as the event handler
```javascript
<Card onClick={() => this.onDishSelect(dish)}>
```
### Lifting State Up
_Move the state to the common ancestor to make sure any state changes will be sent back up to the ancestor_
- Several components may share the same data
- Changes to data in one component needs to be reflected in another component

### Lists and Keys
- Keys should be given to elements inside the array, to help identify which items have changed

### Lifecycle Methods
- Mounting: after creation
- Updating
- Unmounting: no longer needed, unmount from the hierarchy

#### Mounting
_Called when an instance of a component is being created and inserted into the DOM_
- constructor()
- getDerivedStateFromProps()
- render()
- componentDidMount(): use when need to execute something after component gets added into the DOM

Deprecated Method:
- componentWillMount()

#### Updating
_Called when a component is being re-rendered, can be caused by changes to props/state_
- getDerivedStateFromProps()
- shouldComponentUpdate(): return Boolean, if False - inform react's rendering process that this component will never update, so no need to consider when re-rendering
- render(): called when every time the component is re-rendered
- getSnapshotBeforeUpdate(): e.g. retain the scrolling position when scrolling
- componentDidUpdate()

Deprecated methods:
- componentWillReceiveProps()
- componentWillUpdate()

## React Component Types
- Presentational vs Container
- Skinny vs Fat
- Dumb vs Smart
- Stateless vs Stateful

### Presentational and Container Components
#### Presentational Components
_Rendering the view based on the props passed to them_
- Do not maintain local state
- Can be relaxed to maintain only UI state than data

#### Container Components
_Make use of the presentational components for rendering and pass props to them, responsible for storing the state_
- Data fetching, state updates
- Can wrap presentational components in wrapping divs

### Class Component
- Extend React.Component to get class COMPONENTS
- Need to implement the render() method to return the view
- Can have local state
- Lifecycle hooks

### Functional Component
_Simplest way to define React components_
- Returns a React element or a collection of elements that define the view
- Receives a "props" as a parameter
- Cannot have local state or access lifecycle hooks

Method 1:
```javascript
function RenderMenuItem({ dish, onClick }) {
  return ( ... );
} 
```
Method 2: make use of another functional component
```javascript
const Menu = (props) => {
  const menu = props.dishes.map((dish) => {
    return (
      <div key={...} className="...">
        <RenderMenuItem dish={...} onClick={...} />
      </div>
    );
  });
}
```




















