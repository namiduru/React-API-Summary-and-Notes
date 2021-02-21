## **React Hooks**

<br/>

### **_Summary_**

- Comes into the play with React 16.8 version.
- React Native supports as well since version 0.59.
- Use state and other features with functional components.
  - Hooks are functions to hook into states, React life cycle methods and some React features.
- Backward competible.

<br/>

### **_Why?_**

- Use stateful logic without changing your component hierarchy.

<br/>

### **_Rules_**

- This plugin will help you to follow the rules.

```sh
  npm install eslint-plugin-react-hooks --save-dev
```

- Hooks don't work inside class.
- Don't call hook from regular functions.
- These packages all needs to be updated to use Hooks.
  - React Dom, React Native, React DOM Server, React Test Renderer, React Shallow Renderer
- Don't call inside loops, conditions or nested function.

<br/>

### **_Custom Hooks_**

- As convention type 'use' at the beginning of the functions, this way helps you to follow up hook rules while using or declaring a function.

<br/>

### <b style="color: rgb(231,76,60);">API</b>

---

</br>

### <b><i style="color: rgb(52,73,94);">useState</i></b>

**Regular Declaration**

```js
const [name, setName] = useState("mehmet");
```

**If you want to compute a new state using the previous state**

```js
setName((prevState) => prevState + "namiduru");
```

**If initialize a state is expensive operation use this (only executed in initial render)**

```js
const [name, setName] = useState(() => {
  const initalState = generatingName();
  return initialState;
});
```

**If initialize a state is expensive operation use this (only executed in initial render)**

You may consider to useMemo, if you have expensive calculations while rendering.

</br>

### <b><i style="color: rgb(52,73,94);">useEffect</i></b>

**Regular Declaration**

- Run after render
- By default runs after every completed render
- Be careful using useEffect and useLayourEffect on server rendering.
  - Because these will not work but they may effect your final DOM.
- Fires after layout and paint
  - If you want to read DOM then synchoronously re-render use <b><i style="color: rgb(52,73,94);">useLayoutEffect</i></b> hook.
  - Runs like componentDidMount() and componentDidUpdate()
- Passing empty array as second parameter
  - To make sure mount and unmount only once (on mount and unmount)

```js
useEffect(() => {
  return () => {
    // For Clean Up
    /* 
      It is executed when component unmounts or
        on re-rendering to clear up previous effects
    */
  };
}, [props.name]); // useEffect() will only trigger if props.name changes
```

</br>

### <b><i style="color: rgb(52,73,94);">useContext</i></b>

- When nearest provider updates, this hook will trigger a renderer even if React.memo or shouldComponentUpdate exists.
- Will always re-render when context value changes.

```js
const DarkContext = createContext("defaultValue");

// New Way
const ChildAppWithHook = () => {
  const context = useContext(DarkContext);

  return <div>{context}</div>;
};

// Old Way
const ChildComponentWithoutHook = () => {
  return <DarkContext.Consumer>{(value) => value}</DarkContext.Consumer>;
};

ReactDOM.render(
  <>
    <DarkContext.Provider value={"someValue"}>
      <ChildAppWithHook />
      <ChildComponentWithoutHook />
      <App />
    </DarkContext.Provider>
  </>,
  rootElement
);
```

</br>

### <b><i style="color: rgb(52,73,94);">useReducer</i></b>

- useState alternative accepts reducer, state or optionaly state initialization function.
  - Returns state ready only value and dispatch function.
- If same value has returned from Reducer Hook, re-rendering will not happening by this prop.

**Regular Declaration**

```js
const lifeStatus = { life: "good" };

function lifeReducer(state, action) {
  switch (action.type) {
    case "corona-virus":
      return {
        life: "bad",
      };
    case "well-paid-new-job":
      return {
        life: "amazing",
      };
    default:
      throw new Error();
  }
}

function lazyLoading(lifeStatus) {
  return { life: lifeStatus };
}

export default function App() {
  // You could make lazy initialization by passsing third argument as a function and this funciton will take the useReducer's state argument which is lifeStatus in here
  // const [state, dispatch] = useReducer(lifeReducer, lifeStatus, lazyLoading);

  const [state, dispatch] = useReducer(lifeReducer, lifeStatus);

  return (
    <div>
      <h1>My life status</h1>

      <button onClick={() => dispatch({ type: "corona-virus" })}>
        Corona Virus
      </button>
      <br></br>
      <button onClick={() => dispatch({ type: "well-paid-new-job" })}>
        Well Paid New Job
      </button>

      <br></br>
      <br></br>

      {state.life}
    </div>
  );
}
```

</br>

### <b><i style="color: rgb(52,73,94);">useCallback and useMemo</i></b>

- Useful for optimizing generated values from functions to prevent calling functions everytime on rendering phase. (useMemo)
- Useful for childeren component optimization for preventing re-rendering on prop changes. (useCallback)
- Do not use for side effects
  - Because it runs while rendering so it does not have a semantic guarantee.

**useCallback**

- Returns Function

```js
const callBack = useCallback(() => {
  generateName(name);
}, [name]);
```

**useCallback**

- Returns Value

```js
const value = useMemo(() => generateName(name), [name]);
```

</br>

### <b><i style="color: rgb(52,73,94);">useRef</i></b>

- Access a child imperatively
- Accessing child DOM from parent component actions.

```js
const refName = useRef(null);
const focusMyName = () => {
  refName.current.focus();
};
return (
  <>
    <input ref={refName} type="text" />
    <button onClick={focusMyName}>Focus My Name</button>
  </>
);
```

</br>

### <b><i style="color: rgb(52,73,94);">useImperativeHandle</i></b>

- New way of using forwardRef

```js
function FancyInput(props, ref) {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));
  return <input ref={inputRef} ... />; // This input
}
FancyInput = forwardRef(FancyInput);
// So by this implementation any component renders FancyInput could access FancyInput's input focus by referenceOfTheFancyInputInsidePArent.current.focus()
```

</br>

### <b><i style="color: rgb(52,73,94);">useDebugValue</i></b>

- Useful while debugging custom Hooks
- Sometimes you need to format your code before displaying in such cases you may pass function to formating occur only while inspectecting to prevent performance issues.

```js
useDebugValue("Hello this is debugging");

useDebugValue((json) => JSON.parse(json));
```
