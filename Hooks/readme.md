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

</br>

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

</br>

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
