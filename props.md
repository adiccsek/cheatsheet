```html
<template>
  <div>
    <h2>Hello, {{ name }}!</h2> 
    <p>You are {{ age }} years old.</p>
  </div>
</template>

<script>
export default {
  name: "UserGreeting",

  // Define props that the component accepts
  props: {
    name: {
      type: String,
      required: true
    },
    age: {
      type: Number,
      default: 18
    }
  }
};
</script>

<style>
</style>

```
#### Usage:
```
<UserGreeting name="Alice" :age="25" />
```
#### Output:
```
Hello, Alice!
You are 25 years old.
```

#### Explanation:

-   props is an object that defines the inputs this component expects.
-   name is a required string prop.
-   age is a number prop with a default value of 18.
-   Inside the template, these props are accessed with {{ name }} and {{ age }}.