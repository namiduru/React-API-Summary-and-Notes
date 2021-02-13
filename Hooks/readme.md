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

### **_API_**
