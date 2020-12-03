---
title: Simple Calculator
---


# Task definition

Extend the calculator with functions for multiplication and division.

# Installation/setup instructions

1. Download the unpacked zip file to an easy-to-find location (e.g., your Desktop).

2. Open a Terminal window (macOS, Linux) or a cmd window (Windows).

3. In the Terminal/cmd window, use the ```cd``` (change directory) command to change to the unpacked directory.

> i.e., if you unpacked the zip file to the desktop, you have to use


> ```
> cd ~/Desktop/simple_calculator
> ```

> on the Mac, or

> ```
> cd Desktop\simple_calculator
> ```

> on Windows.


4. Type the following command

> ```
> npm install
> ```

> Explanation: This installs all the required additional code to run your application.

5. Open the Visual Studio Code editor in the current directory

> ```
> code .
> ```

6. Start the local development web server

> ```
> npm run serve
> ```

> After that, you should be able to open ```http://localhost:8080/``` in your browser. > You should see the calculator application with addition and subtraction.

# A tour of the code

Open the file ```src/App.vue``` in the editor. This file is a Vue component, and it's divided into three sections that contain

1. The UI elements (`template`)
2. The functionality (`script`)
3. Styling/CSS (`style`)



Let's have a look at the three sections.


## Template

```html
<template>
<h1>Simple calculator</h1>
    <p>
        <label for="number1">Number 1:</label>
        <input name="number1" v-model.number="number1" type="number">
    </p>
    <p>
        <label for="number2">Number 2:</label>
        <input name="number2" v-model.number="number2" type="number">
    </p>
    <button v-on:click="add">Add</button>
    <button v-on:click="subtract">Subtract</button>
    <p>
        <label for="result">Result:</label>
        <input name="result" v-model.number="result" readonly type="number">
    </p>
</template>
```

Let's analyse the code inside the first `<p>....</p>` section.

```html
<p>
    <label for="number1">Number 1:</label>
    <input name="number1" v-model.number="number1" type="number">
</p>
```

The `input` element creates the input box for the first number. We also set the `name` attribute of the `input` to the name `number1`, because this is used by the `label` element to visually align the two elements. We also set the `type` attribute to `number` to prevent users from entering anything except actual numbers. 

Now, let's look at `v-model.number="number1"`: This establishes a connection between the input box element that you can see on the web page and the data element `number1` (see below in the `script` section). The two are bound together - whenever the data in the input box changes, the data element is updated as well. Another way to think of it is that the data attribute `number1` is a `model` of the user interface element.

Note that we have also added a `.number` specification to the `v-model` directive - this informs the vue.js framework that it should treat the data coming from this element as numbers. Without this, values would be treated as strings, and if two strings are added in JavaScript, they are actually concatenated (so `2+3` would result in `23` instead of `5`, which is the mathematically correct result of adding those two numbers).


In the second `<p>...</p>` block, the input element for the second number is set up, and it works exactly the same way as for `number1`; however, the names and the referenced data attribute are changed to `number2`, as you can see in the code.

Now let's continue with the button elements:

```html
<button v-on:click="add">Add</button>
```

This creates a button with the label `Add`. Look at the code `v-on:click="add"` - this means: Whenever the button is clicked, call the `add` function (see below in the script section).

`v-on` is a special directive that can be used to listen for events; there are all kinds of events in HTML, but here we are only interested in the `click` event which happens if the user clicks the button with the mouse.


Finally, there is a third `<p>...</p>` section containing an `input` element.

```html
<p>
    <label for="result">Result:</label>
    <input name="result" v-model.number="result" readonly type="number">
</p>
```

Here, the element is bound to the `result` data element (`v-model.number="result"`). The element is set to `readonly` because it only shows the result of the calculation. 


## Script

```js
<script>
export default {
  name: 'App',
  data () {
    return {
      number1: 0,
      number2: 0,
      result: 0
    }
  },
  methods: {
    add () {
      this.result = this.number1 + this.number2
    },
    subtract () {
      this.result = this.number1 - this.number2
    }
  }
}
</script>
```

The script section defines the functionality of your application; a minimal script section would be

```js
export default {
    name: 'App'
}
```
Because we also need data and functionality, we add
1. a data function (provides all the data items/variables for your application)
2. a methods object (provides the required functions)

Extending the app:

```js
export default {
    name: 'App',
    data () {
    },
    methods: {
    }
}
```

Now let's think about the data elements that are necessary for the calculation. We need
1. `number1`
2. `number2`
3. `result`

Adding this to the app and initialising all data elements with 0:

```js
export default {
    name: 'App',
    data () {
        number1: 0,
        number2: 0,
        result: 0
    },
    methods: {
    }
}
```

Now, let's think about the functionality. We need
1. addition
2. subtraction

So let's add two functions:

```js
export default {
    name: 'App',
    data () {
        number1: 0,
        number2: 0,
        result: 0
    },
    methods: {
        add () {
        },
        subtract () {
        }
    }
}
```

However, those functions don't do anything yet. So what should they do?

1. `add` should sum `number1` and `number2`
2. `subtract`should subtract `number2` from `number1`

The results should go into the data element `result`. Here is the implementation of this functionality:

```js
export default {
    name: 'App',
    data () {
        number1: 0,
        number2: 0,
        result: 0
    },
    methods: {
        add () {
            this.result = this.number1 + this.number2
        },
        subtract () {
            this.result = this.number1 - this.number2
        }
    }
}
```


## Style

Style contains some CSS (Cascading Style Sheets) definitions. You can ignore it for the time being.

```css
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
}

label {
  margin: 3px;
  width: 100px;
  display: inline-block;
  text-align: end;
}

input {
  margin: 3px;
  width: 200px;
}
button {
  margin: 3px;
}
</style>

```

# To do

Open the file 'src/App.vue' in the code editor.

Add two buttons for multiplying and dividing numbers to the `template` section. The corresponding HTML code should go to the section between these comments:

```
<!-- 
  TODO
  Add the buttons for multiplication and division here
 -->



<!-- End TODO -->
```

Then add two functions that implement the required functionality to the `script` section. The functions should go to the section between those comments:

```
/*
    TODO

    Add the functions for multiplication and division here
*/



/*
    End TODO
*/
```

# Note

Don't hesitate to contact me by [email](mailto:martin.gasser@uni-ak.ac.at) if you have questions, problems, or suggestions.