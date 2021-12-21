# Vue.js_evolution
- [Vue.js_evolution](#vuejs_evolution)
  - [Create a simple project](#create-a-simple-project)
  - [Project Structure](#project-structure)
  - [Binding Text](#binding-text)
  - [Binding HTML](#binding-html)
  - [Binding Attributes](#binding-attributes)
  - [Binding Classes](#binding-classes)
  - [Binding Styles](#binding-styles)
  - [Binding  Shortcut](#binding--shortcut)
  - [Conditional Rendering](#conditional-rendering)
  - [List Rendering](#list-rendering)
      - [Key attribute:](#key-attribute)
      - [V-for Directive](#v-for-directive)
  - [Methods](#methods)
  - [Event Handing](#event-handing)
      - [Form Handing](#form-handing)
      - [Capture user inputs](#capture-user-inputs)
      - [Text-areas](#text-areas)
      - [Single select dropdown control](#single-select-dropdown-control)
      - [Multi select control](#multi-select-control)
      - [Checkbox](#checkbox)
      - [CheckBox Group](#checkbox-group)
      - [Radio](#radio)
      - [Submit form data](#submit-form-data)
  - [Modifiers](#modifiers)
  - [Bonus Directives](#bonus-directives)
  - [Computed](#computed)
    - [Use Computed :](#use-computed-)
    - [Computed vs Methods](#computed-vs-methods)
    - [Computed and v-for](#computed-and-v-for)
    - [Computed Setter](#computed-setter)
  - [Watchers](#watchers)
    - [Use watchers when:](#use-watchers-when)
  - [Components](#components)
    - [Component Props](#component-props)
    - [Prop types and Validation](#prop-types-and-validation)
    - [Non-Props Attributes](#non-props-attributes)
    - [Provide/Inject](#provideinject)
    - [Component Events: Child talks to parent](#component-events-child-talks-to-parent)
    - [Validating Emitted Events](#validating-emitted-events)
    - [Components and v-model](#components-and-v-model)
  - [Slots](#slots)
    - [named Slot : multiple slots](#named-slot--multiple-slots)
    - [Slots props](#slots-props)
  - [Component  Styles](#component--styles)
  - [Dynamic Components](#dynamic-components)
    - [Keeping Dynamic component Alive](#keeping-dynamic-component-alive)
  - [Teleport Component](#teleport-component)
  - [Vue and HTTP](#vue-and-http)
  - [Component Lifecycle Hooks](#component-lifecycle-hooks)
  - [Template Refs](#template-refs)
  - [Reusability with Mixins](#reusability-with-mixins)
  - [Composition Api](#composition-api)
    - [Why Composition API](#why-composition-api)
      - [### Example Code](#-example-code)
      - [Replacing data with ref](#replacing-data-with-ref)
      - [Replacing methods and examples](#replacing-methods-and-examples)
      - [Composition with V-model example](#composition-with-v-model-example)
      - [Replacing computed Method example](#replacing-computed-method-example)
      - [Replacing watch example](#replacing-watch-example)
      - [Replacing provide/Inject](#replacing-provideinject)

## Create a simple project

1. yarn global add @vue/cli

2. vue create hello-world

3. cd hello-world

4. yarn serve

## Project Structure

1. A *.Vue file is a custom file format that uses HTML-Like syntax to describe a portion of the UI

2. Each *.Vue file consists of tree types of top-level language blocks
   
   1. <template> </template>
   
   2. <script></script>
   
   3. <style></style>

3. The template Block is like HTML of your UI

4. The Script Block is where the logic and functionality of your app can be maintained

5. The CSS block is where you specify the style related to the mark up in the template block

## Binding Text

```javascript
<template>
  <div>{{greet}} {{ name }}</div>
  <div v-text="channel"></div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      greet: "hello",
      name: "Batman",
      channel: "Volution"
    };
  }
}
</script>
```

* Two ways to blinding Text
  
  ```javascript
  <div>{{greet}} {{ name }}</div> // recommanded
  // it will overwrite children text
  //  only full text
  <div v-text="channel"></div>  
  ```

## Binding HTML

```javascript
// Only Blinding HTML by trust source
 <div v-html="channel"></div>
export default {
  data() {
    return {
      channel: "<b>Volution</b>"
    };
  }
}
```

## Binding Attributes

```javascript
  data() {
    return {
      headingId: "heading",
      IsDisabled: true
    };

 <h2 v-bind:id="headingId">header</h2>
 <button v-bind:disabled="IsDisabled">Bind</button>

 <h2 id="heading">header</h2>
 <button disabled>Bind</button>
```

Through the `v-bind` to add some attributes to the html

## Binding Classes

Binding the class from the data attribute

```javascript
<h2 v-bind:class="status"> Status</h2>
<h2 class="underline" v-bind:class="status">Underline text</h2>
// if isPromoted is true, then Do `promoted`
<h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2> 
// if isPromoted is false, then do Nothing
<h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2> 
// if the isSoldout is fase, then new 
<h2 v-bind:class="isSoldout? 'sold-out' :  'new'">Soldout? movie</h2>
// if the isSoldout is true, then sold-out
<h2 v-bind:class="isSoldout? 'sold-out' :  'new'">Soldout? movie</h2>
// take array of classes which appied to the object
<h2 v-bind:class="['new', 'promoted']">Newly promoted movie</h2>
// conditonal Array
<h2 v-bind:class ="[isPromoted && 'promoted', isSoldout ? 'sold-out' : 'new']">Array Contional movie</h2>
// Object 
<h2 v-bind:class="{
     promoted: isPromoted,
     new: !isSoldout,
     'sold-out': isSoldout
   }">Object conditional Movie</h2>

<h2 class="danger"> Status</h2>
<h2 class="promoted">Promoted Movie</h2>
<h2>Promoted Movie</h2>
<h2 class="new">Soldout? movie</h2>
<h2 class="new promoted">Newly promoted movie</h2>
```

## Binding Styles

```javascript
  <h2 v-bind:style="{
     color: highlightColor,
     fontSize: headerSize + 'px',
     padding: '20px'
   }">Inline Style</h2>

   <h2 v-bind:style ="styleObject">Inline Object</h2>
```

we  also can applied the array of binding classes. Last element have higher priority.

## Binding  Shortcut

```javascript
<h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2>
// is as same as below
<h2 :class="isPromoted && 'promote4645d'">Promoted Movie</h2>
```

```javascript
<template>
  <h2 v-bind:id="headingId">header</h2>
  <button v-bind:disabled="IsDisabled">Bind</button>
  <h2 class="underline">Underline text</h2>
    <h2 v-bind:class="status"> Status</h2>
   <h2 class="underline" v-bind:class="status">Underline text</h2>
   <h2 v-bind:class="isPromoted && 'promoted'">Promoted Movie</h2>
   <h2 v-bind:class="isSoldout? 'sold-out' :  'new'">Soldout? movie</h2>
   <h2 v-bind:class="['new', 'promoted']">Newly promoted movie</h2>
   <h2 v-bind:class="[isPromoted && 'promoted', isSoldout ? 'sold-out' : 'new']">Array Contional movie</h2>
   <h2 v-bind:class="{
     promoted: isPromoted,
     new: !isSoldout,
     'sold-out': isSoldout
   }">Object conditional Movie</h2>
   <h2 v-bind:style="{
     color: highlightColor,
     fontSize: headerSize + 'px',
     padding: '20px'
   }">Inline Style</h2>

   <h2 v-bind:style ="styleObject">Inline Object</h2>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      headingId: "heading",
      IsDisabled: true,
      status: 'danger',
      isPromoted: false,
      isSoldout: true,
      highlightColor: 'orange',
      headerSize: 50,
      styleObject: {
        color: 'orange',
        'font-size': '50px'
      },

    };
  }
}
</script>
```

## Conditional Rendering

if - else statement

```javascript
<template>
  <h2 v-if="num === 0">The number is zero</h2>
  <h2 v-else-if="num > 0">The number is positive</h2>
  <h2 v-else-if="num < 0">The number is negative</h2>
  <h2 v-else>it is not a number</h2>
  <div>
    <h2>Vishwas</h2>
    <h2>Codevolution</h2>
    <h2>Vue</h2>
  </div>
</template>
```

There is potential error: it may cause the layout is wrong

```javascript
 // in the html, the <div> will display
 <div>
    <h2>Vishwas</h2>
    <h2>Codevolution</h2>
    <h2>Vue</h2>
  </div>
```

way to solve it:

```javascript
  <template v-if="display">
    <h2>Vishwas</h2>
    <h2>Codevolution</h2>
    <h2>Vue</h2>
  </template>
```

There is extra method: `v-show`

```javascript
<h2 v-show="showContext">show the showContext</h2>
```

what is different between `v-if` and `v-show`

* `v-if` it will mount or dis-mount

* `v-show` it will be generate on UI

```javascript
<template>
  <h2 v-if="num === 0">The number is zero</h2>
  <h2 v-else-if="num > 0">The number is positive</h2>
  <h2 v-else-if="num < 0">The number is negative</h2>
  <h2 v-else>it is not a number</h2>
  <template v-if="display">
    <h2>Vishwas</h2>
    <h2>Codevolution</h2>
    <h2>Vue</h2>
  </template>

<h2 v-show="showContext">show the showContext</h2>
</template>
```

## List Rendering

#### Key attribute:

* The key special attributes is primarily used as hint for Vue's virtual DOM algorithm to identify nodes when diffing the new list of nodes against the old list

* When used with the v=for directive, the key attribute should always have a unique value in each iterator 

* without keys, Vue uses an algorithm that minimizes element movement and tries to patch/reuse elements of the same type in place as much as possible 

* Not using keys is only suitable when your list render output does not rely on temporary Dom state or child component state

* Although the default behavior of patching is more efficient, it can lead to problems

* a typical value to provide to the key attribute is the id property is an Object. But any unique property will do as long as its not non-primitive value like Object or arrays

#### V-for Directive

1. Array of Strings 
   
   ```javascript
   <h2 v-for="name in names" v-bind:key="name">{{ name }}</h2>
   // generaete index 
   <h2 v-for="(name,index) in names" v-bind:key="name">{{ index }} {{ name }}</h2>
   ```

2. Array of Objects
   
   ```javascript
   <h2 v-for="name in fullName" :key="name.first">{{ name.first }} {{name.last}}</h2>
   ```

3. Array of arrays
   
   ```javascript
   <h2 v-for="(value, key, index) in myInfor" :key="value">{{index}} {{key}} {{ value}}</h2>
   //0 name Vishwas
   //1 channel CodeVolution
   ```
   
   ```javascript
   <div v-for="actor in actors" :key="actor.name">
     <h2>{{ actor.name}}</h2>
     <h3 v-for="movie in actor.movies" :key="movie">{{movie}}</h3>
   </div> 
   ```

4. Block of HTML elements
   
   ```javascript
   <template v-for="name in names" :key="name">
     <h2>{{name}}</h2>
     <hr />
   </template>
   ```

5. conditional List Rendering
   
   note that `v-for`can not write with `v-if` in the same line. `v-if`has the higher priority
   
   ```javascript
    <template v-for="name in names" :key="name">
       <h2 v-if="name === 'Bruce'"> {{name}}</h2>
     </template>
   ```
   
   ```javascript
   <template>
     <!-- <h2 v-for="name in names" v-bind:key="name">{{ name }}</h2> -->
     <h2 v-for="(name,index) in names" v-bind:key="name">{{ index }} {{ name }}</h2>
     <h2 v-for="name in fullName" :key="name.first">{{ name.first }} {{name.last}}</h2>
   
     <div v-for="actor in actors" :key="actor.name">
       <h2>{{ actor.name}}</h2>
       <h3 v-for="movie in actor.movies" :key="movie">{{movie}}</h3>
     </div>
   
     <h2 v-for="(value, key, index) in myInfor" :key="value">{{index}} {{key}} {{ value}}</h2>
   
     <template v-for="name in names" :key="name">
       <h2 v-if="name === 'Bruce'"> {{name}}</h2>
     </template>
   
   <template v-for="name in names" :key="name"> 
     <h2>{{name}}</h2>
     <hr />
   </template>
   ```

## Methods

ways to create method:

```javascript
<h2>Add method -- {{add()}} </h2>
<h2>Add method -- {{add1(1,2,3)}} </h2>
// this use variable from data, then `this`
 <h2>Add method -- {{multiply(10)}} </h2>
```

## Event Handing

Two type `button`:

1. `v-on:click`
   
   ```javascript
   <button v-on:click = "count += 1">{{ count }}</button>
   ```

2. `v-on:mouseover`:
   
   ```javascript
   <button v-on:mouseover = "increase()">count </button>
   ```

ShortHand syntax

1. `v-on:` -> `@`
   
   ```javascript
   <button @click = "count += 1">{{ count }}</button>
   ```

2. `changeName(event)`
   
   vue auto pass in event object 

#### Form Handing

```javascript
<form @submit="submitForm">
</form>
```

#### Capture user inputs

```javascript
<div>
      <label for="name"> name </label>
      <input type="text" id="name" v-model.trim.lazy="formValues.name"/>
    </div>
```

#### Text-areas

```javascript
 <div>
      <label for="profile">Profile Summary.trim.lazy</label>
      <textarea id="profile" v-model="formValues.profileSummary"/>
    </div>    
```

#### Single select dropdown control

```javascript
<div>
      <label for="country">Country</label>
      <select id = "country" v-model="formValues.country">
        <option value= "">Select a country</option>
        <option value= "india">India</option>
        <option value= "Singapore">Singapore</option>
      </select>
    </div>
```

#### Multi select control

```javascript
<div> 
      <label for="job-location">Job Location</label>
      <select id = "job-location" multiple v-model="formValues.jobLocation">
        <option value= "india">India</option>
        <option value= "Singapore">Singapore</option>
      </select>
    </div>
```

#### Checkbox

```javascript
  <div>
      <input type="checkbox" id="remotework" v-model="formValues.remoteWork"/>
      <label for="remoteWork">Open to remote work?</label>
    </div>
```

#### CheckBox Group

```javascript
 <div>
      <label>Skill Set</label>
      <input type="checkbox" id="html" v-model="formValues.skillSet" value="html" />
      <label for="html">HTML</label>
      <input type="checkbox" id="css" value="css" v-model="formValues.skillSet" />
      <label for="css">CSS</label>
      <input type="checkbox" id="javascript" value="javascript" v-model="formValues.skillSet" />
      <label for="javascript">Javascirpt</label>
    </div>
```

#### Radio

```javascript
  <div>
      <label>years of Experience</label>
      <input type="radio" id="0-2" value="0-2" v-model="formValues.yearsOfExperience"/>
      <label for="0-2">0-2</label>
    </div>
```

#### Submit form data

```javascript
  <div>
      <button>Submit</button>
    </div>
```

```javascript
export default {
  name: 'App',
  data() {
    return {
      formValues: {
        name: "",
        profileSummary: "",
        country: "",
        jobLocation: [],
        remoteWork: false,
        skillSet: [],
        yearsOfExperience: "",
        age: null,
      }
    };
  },
  methods: {
    submitForm(event) {
      event.preventDefault()
      console.log("form value", this.formValues)
    }
  },
}
```

## Modifiers

a suffix you can add to either the v-on directive or the v-model directive to add some functionality inline within the template

Helps you write cleaner code

1. `ignore the all empty sapce`:         `.trim`

2. `number modifer`:           `.number` 

3. `lazy modifer`:               `accept input after fill out`

4. `prevent refreash`       `.prevent`

5. `@keyup.enter="sibmbitForm"`    `after input, directly submit`

## Bonus Directives

1. `v-once`:  only render once

2. `v-pre`:   Skips compilation for the corresponding element

## Computed

properties that can be bound to the template like data properties

They are used for composing new data from existing sources

They are highly performant as they are cached calculations which only update when their dependencies change 

### Use Computed :

1. You need to compose new data from existing data source

2. You need to reduce the length of a variable 

```javascript
<h2>
    Total - {{ items.reduce((total, curr) => (total = total + curr.price),0)}}
  </h2>
  <h2>Computed Total - {{total}}</h2>
// rather than computed each time, computed to a method
computed:{
    fullName(){
      return `${this.firstName} ${this.lastName}`
    },
    total(){
      return this.items.reduce((total, curr) => (total = total + curr.price), 0)     
    }
  }
```

Simple use-age: add button:

```javascript
<button @click="items.push({id: 4, title: 'keyboard', price: 50})">Add</button>
```

### Computed vs Methods

methods don't know if the values used in the function changed so **they need to run every-time to check**. computed properties know if the values used in the function changed so **they don't need to run every-time to check, only once!**

For example: input box for methods: if we input `life`, the method will generate 4 times.

### Computed and v-for

Two ways to display `item greater than 200`

```javascript
<template v-for="item in items" :key="item.id">
    <h2 v-if="item.price >= 200">
      {{item.title}} {{item.price}}
    </h2>
  </template>
```

Even though it works well, but it recommend to use computed method. Save it in the cache

```javascript
  computed:{
    expensiveItem() {
      return this.items.filter(item => item.price > 100)
    }
  }
  <h2 v-for="item in expensiveItem" :key="item.id">{{item.title}} {{item.price}}</h2>
```

display a list of item, computed property is good way to do that.

### Computed Setter

Work for read and write 

```javascript
<template>
  <h2>FullName - {{firstName}} {{lastName}}</h2>
  <h2>computed fullname - {{fullName}}</h2>
  // it will call the `changeFullName` method
  <button @click="changeFullName">change name</button>
</template>

<script>
export default {
methods: {
    changeFullName(){
       // it will pass 'Clark kent' to the set method
      this.fullName = 'Clark Kent'
    }
  }, 
  computed:{
    fullName: {
      get(){
        return `${this.firstName} ${this.lastName}`
      },
      set(value){
        const names = value.split(' ')
        this.firstName = names[0],
        this.lastName = names[1]
      },
    }
}
</script>
```

## Watchers

To track the data 

### Use watchers when:

1. You have to check if a property has changed to a favorable value to know if you're ready to perform an action

2. You have to call an APP in response to change in application data 

3. you have to apply transitions

```javascript
<template>
  <h2>Volume tracker</h2>
  <h3>Current Volumn = {{ Volume }}</h3>  
  <div>
    <button @click="Volume += 2">Increase</button>
    <button @click="Volume -= 2">Decrease</button>
  </div>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      Volume: 0
    };
  },
  methods: {}, 
  computed:{},
  watch:{ 
   // it should as same as the data varible, so the wacter can track it
   // second paramter as pervious value
    Volume(newValue, oldValue){
       if (newValue === 16){
         alert("it is error")
       }
    }
  }
}
</script>
```

getting deeper: watcher execute only the data has changed.  After the re-fresh the api would not call. 

Step1: set the watcher run after the page re-fresh

```javascript
watch:{
    // set the movie becomes Object
    movie: {
      handler(newValue) {
        console.log(`Calling the Api with movie = ${newValue}`)
      },
      // set true after the page re-load
      immediate: true,
    }
  }
```

Step2: watcher would not watch for changes in deeply nested properties by default

Object and Array

```javascript
<template>
  <h2>Volume tracker</h2>
  <h3>Current Volumn = {{ Volume }}</h3>  
  <div>
    <button @click="Volume += 2">Increase</button>
    <button @click="Volume -= 2">Decrease</button>
  </div>
  <input v-model="movie" />
  <input v-model="movieInfo.title" />
  <input v-model="movieInfo.actor" />
  <button @click="movieList.push('wonder woman')">add</button>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      Volume: 0,
      movie: 'BatMan',
      movieInfo: {
        title: '',
        actor: ''
      },
      movieList: ['batman','superman']
    };
  },
  methods: {}, 
  computed:{},
  watch:{
    Volume(newValue){
       if (newValue === 16){
         alert("it is error")
       }
    },
    movie: {
      handler(newValue) {
        console.log(`Calling the Api with movie = ${newValue}`)
      },
      immediate: true,
    },
    movieInfo: {
      handler(newValue) {
        console.log(`Calling the Api ${newValue.title} and ${newValue.actor}`)
      },
      // diaplay the nested obejct
      deep: true
    },
    movieList: {
      handler(newValue) {
        console.log(newValue)
      },
      deep: true
    }
  }
}
</script>
```

## Components

Component contains:  template, script, style

```javascript
// html
<template>
    <h2>Hello, Jeffrey</h2>
</template>

// method
<script>
export default {
    name: 'Greet'  // what is the name of current component
}
</script>
```

How to the call the component in Vue.app

```javascript
//create a component in html file
<template>
  <Greet />
</template>

<script>
import Greet from './components/Greet.vue' // import the component

export default {
  name: 'App',
  components: {
    Greet,     // name of components 
  }
}
</script>
```

### Component Props

```javascript
<template>
  <Greet name = 'Burce'/>  // put name attribute with value Burce
  <Greet name = 'Clark'/>
  <Greet :name = 'name'/>
</template>

<script>
import Greet from './components/Greet.vue'

export default {
  name: 'App',
  components: {
    Greet,
  },
  data() {
    return {
      name: 'batman'    // can use static props
    }
  }
}
</script>
```

Children component:

```javascript
<template>
    <h2>Hello, {{name}}</h2>
</template>

<script>
export default {
    name: 'Greet',
    props: ['name'] // collect the props
}
</script>
```

### Prop types and Validation

pass parameter by type

```javascript
<template>
 //`:like` says that pass the type as required
  // String do not need to this.
  <Article title="good" :like='50' :isPublished="true"/>
</template>
```

Define the prop types and Validation

```javascript
<script>
    export default {
        name: 'Article',
        props: {
            title: {
                String,
                required: true,
                default: 'Article'
            },
            like: Number,
            isPublished: Boolean
        }
    }
</script>
```

### Non-Props Attributes

A non-prop attribute is an attribute that is passed to a component, but does not have a corresponding property defined in the props option

For example: id, class, and style attributes

```javascript
// the id `my-i-attribute` will auto add to the root 
<Article id="my-id-attribute" title='good' :like='50' :isPublished="true"/>
```

```javascript
<template>
    <div>
        <h2>Article Component</h2>
        <h2 v-bind="$attrs">{{title}}</h2>  // add to the children tag
        <h2>{{like}}</h2>
        <h2>{{isPublished}}</h2>
    </div>
</template>

<script>
    export default {
        name: 'Article',
        props: {
            title: {
                String,
                required: true,
                default: 'Article'
            },
            like: Number,
            isPublished: Boolean
        },
        inheritAttrs: false   // avoid the id class add to root
    }
</script>
```

### Provide/Inject

<img src="file:///var/folders/mw/dwlqnlkj4_bbq4q_053kczp80000gn/T/TemporaryItems/NSIRD_screencaptureui_Y5C3Js/Screen%20Shot%202021-12-19%20at%209.48.03%20AM.png" title="" alt="Screen Shot 2021-12-19 at 9.48.03 AM.png" width="496">

The two APIs provide a way to pass data through the component tree without having to pass down props manually at every level

1. Provide the value in the App component

2. Inject the value in the component F

```javascript
// Component C
// To use the variables in the parent
// the the set `provide` as method
<script>
import ComponentE from './ComponentE.vue'
    export default {
        name: 'ComponentC',
        components:{
            ComponentE
        },
        data() {
            return {
                name: 'Jeffrey'
            }
        },
        // provide the value to children 
        provide() {
            return {
                userName: this.name
            }
        }
    }
</script>
```

Children Component

```javascript
<script>
    export default {
        name: 'ComponentF',
        inject: ['userName']
    }
</script>
```

### Component Events: Child talks to parent

<img src="file:///var/folders/mw/dwlqnlkj4_bbq4q_053kczp80000gn/T/TemporaryItems/NSIRD_screencaptureui_VkicFu/Screen%20Shot%202021-12-19%20at%2010.07.35%20AM.png" title="" alt="Screen Shot 2021-12-19 at 10.07.35 AM.png" width="475">

`emits`: send the props to parent

```javascript
<template>
    <div>
        <h2>This is pop up component</h2>
        // the second parameter as the data 
        // first parameter as event name
        <button @click="$emit('close', 'Jeffrey')">Colose popup</button>
    </div>
</template>

<script>
    export default {
        name: 'PopUp',
        emits: ['close'] 
    }
    
</script>
```

```javascript
<template>
  <button @click="isPopUp = true">PopUp</button>
  <PopUp v-show="isPopUp" @close="isPopUp = false"/>
</template>

<script>
import PopUp from './components/PopUp.vue'
export default {
  name: 'App',
  components: {
    PopUp,
  },
  data() {
    return {
      isPopUp: false,
    }
  }
}
</script>
```

Therefore, we can call the custom event in the parent component

**How to pass data into the parent component**

`in the parent create a method`

```javascript
<template>
  <button @click="isPopUp = true">PopUp</button>
  // create the method to handle the data
  <PopUp v-show="isPopUp" @close="ClosedPopUp"/>
</template>

<script>
import PopUp from './components/PopUp.vue'
export default {
  name: 'App',
  components: {
    PopUp,
  },
  data() {
    return {
      isPopUp: false,
    }
  },
  methods: {
     ClosedPopUp(values){
        this.isPopUp = false,
        console.log(values)
     }
  }
}
```

### Validating Emitted Events

```javascript
<template>
    <div>
        <h2>This is pop up component</h2>
        <input type="text" v-model="name"/>
        <button @click="$emit('close', name)">Colose popup</button>
    </div>
</template>

<script>
    export default {
        name: 'PopUp',
       // do some validation on the emits
        emits: {
            // function 
            close: (name) => {
                if (!name) return false
                else return true
            }
        },
        data(){
            return {
                name: '',
            }
        }
    }
    
</script>
```

### Components and v-model

it will `v-model` the variable from component event

```javascript
<template>
    <div>
        <input type='text' :value="modelValue" @input="$emit('update:modelValue', $event.target.value)"/>
    </div>
</template>

<script>
    export default {
        name: 'Input',
        // recieve the props
        props: {
            modelValue: String
        }
    }
</script>

```

## Slots

Props allow you to re-use components by passing in different data 

Although props are great for re-usability, we do have a strict parent-child relationship

the children will always be in control of the HTML content and the parent can only pass in different data values

Slots on the other hand are more powerful

They allow you to re-use a component

they allow the parent component to control the content inside the child content

Slots allow a parent component to embed any content in a child component including HTML elements

```javascript
<template>
    <div>
        <slot>Default Content</slot>
    </div>
</template>

<script>
    export default {
        name: 'Card'
    }
</script>
```

Parent component can simply put any content by `<Card></Card>`

```javascript
<template>
  <Card>Any content can put in slot</Card>
</template>

```

### named Slot : multiple slots

```javascript
<template>
    <div>
        <div>
            <slot name = "header"></slot>
        </div>
        <div>
            <slot ></slot>
        </div>
        <div>
            <slot name = "footer"></slot>
        </div>
    </div>
</template>
```

Parent Component:

```javascript
<template>
  <Card>
    <template v-slot:header> header content</template>
    <template v-slot:default> slot without name content</template>
    <template v-slot:footer> footer content</template>
  </Card>
</template>

```

### Slots props

 Using `slots` to get `data` from children component 

```javascript
<template>
    <div>
        <h3 v-for="name in names" :key="name.firstName">
            <slot :firstName="name.firstName" :lastName="name.lastName"></slot>
        </h3>
    </div>
</template>
```

```javascript
<template>
  <NameList>
    <template v-slot:default="slotProps">
      {{slotProps.firstName}} {{slotProps.lastName}}
    </template>
  </NameList>
</template>
```

## Component  Styles

1.  By default, a component  styles are applied globally in the component tree

2.  Parent style render after the children style 

3.  add`scoped`  attribute ensures a component's CSS will apply only to it's own HTML

4. "With scoped, the parent component's style will not leak into child components. However, a child component's root node will be affected by both  the parent's scoped CSS and the child's scoped CSS. This is by design so that the parent can style the child root element for layout purpose"

5. When using slots, the parent components styles are applied and not the child component styles even though the content is embedded inside the child component

## Dynamic Components

Select corresponding  component

```javascript
<template>
  <button @click="activeTab = 'TabA'">Tab A</button>
  <button @click="activeTab = 'TabB'">Tab B</button>
  <button @click="activeTab = 'TabC'">Tab C</button>
  // after click to pick one 
  <component :is="activeTab" />
</template>
```

### Keeping Dynamic component Alive

* to keep status of in-active component

```javascript
<keep-alive> 
 <component :is="activeTab" />
</keep-alive> 
```

## Teleport Component

use to create model 

## Vue and HTTP

`yarn add axios`

Get request from axios

```javascript
<template>
    <div>   
        <button @click="getPosts">Load Posts</button>
        <div v-for="post in posts" :key="post.id">
            <h3>{{post.id}} {{post.title}}</h3>
            <p>{{post.bod}}</p>
            <hr/>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name:'PostList',
        data(){
            return {
                posts: [],
            }
        },
        methods:{
            getPosts() {
                axios.get('https://jsonplaceholder.typicode.com/posts')
                .then((reponse) => {
                    console.log(reponse.data)
                    this.posts = reponse.data
                })
                .catch(error => {
                    console.log(error)
                })
            }
        }
    }
</script>


```

post request from axios

```javascript
<template>
    <div>
        <form @submit.prevent="createPost">
            <div>
                <label for="userId">Post user id</label>
                <input type="text" id="userId" v-model="fromData.userId"/>
            </div>
             <div>
                <label for="title">Post user id</label>
                <input type="text" id="title" v-model="fromData.title"/>
            </div>
             <div>
                <label for="body">Post user id</label>
                <input type="text" id="body" v-model="fromData.body"/>
            </div>
            <button>Create Post</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name:'CreatePost',
        data(){
            return{
                fromData: {
                    userId: '',
                    title:'',
                    body: ''
                }
            }
        },
        methods: {
            createPost(){
                axios.post('https://jsonplaceholder.typicode.com/posts', this.formData)
                .then(Response => console.log(Response))
                .catch(error => console.log(error))
            }
        }
    }
</script>

<style scoped>

</style>
```

## Component Lifecycle Hooks

A vue component can go through 4 phases

1. Creation

2. Mounting

3. Updating

4. Unmounting

Lifecycle hooks are methods that allow us to hook into or trap into there different phases in the lifecycle of a component and execute some code

![Screen Shot 2021-12-20 at 11.28.28 AM.png](/var/folders/mw/dwlqnlkj4_bbq4q_053kczp80000gn/T/TemporaryItems/NSIRD_screencaptureui_45AdYT/Screen%20Shot%202021-12-20%20at%2011.28.28%20AM.png)

## Template Refs

after the page load, it will focus on the input box

```javascript
<template>
    <div>
        <input type="text" ref="inputRef"/>
    </div>
</template>

<script>
    export default {
        name: 'TemplateRef',
        mounted(){
           this.$refs.inputRef.focus()
        }
    }
</script>

<style scoped>

</style>
```

## Reusability with Mixins

1. Create a `Minxins` folder

2. Create file with `.js`  javaScript file

3. create `script's data() and methods`

4. import it into the component 

5. `mixinx:[import name]`

Component's variable can overwrite the variable in the `mixinx`



## Composition Api

The composition Api is a feature in Vue 3 which gives us another way to write our components

Options API - data(), computed properties, methods, watchers & lifecycle hooks

### Why Composition API

1. Vue projects become hard to manage as they grew in size and complexity

2. Re-using logic across components becomes difficult

The composition API allows us to encapsulate one piece of functionality so that you can use it in different components throughout the application

#### ### Example Code

#### Replacing data with ref

hightLights: 

1. Refs returns a reactive and mutable object  that serves as a reactive reference to internal value
   
   Use ref() for primitive data types like string, boolean, number, null, undefined, symbol And use reactive() for non-primitive data types like array, object.

2. `toRefs`: return the reactive objects

#### Replacing methods and examples

#### Composition with V-model example

#### Replacing computed Method example

#### Replacing watch example

#### Replacing provide/Inject

[Vue JS 3 Tutorial - 60 - Replacing Provide/Inject - YouTube](https://www.youtube.com/watch?v=VS7Qy0TYtN0&list=PLC3y8-rFHvwgeQIfSDtEGVvvSEPDkL_1f&index=60)



```javascript
<template>
    <div>
        <h2>{{ name }}</h2>
        <input type="text" v-model="name"/>
        <button @click="IncreaseCount">{{ count }}</button>
        <h2>{{first}} {{last}}</h2>
        <button @click="changeName">change name</button>
        
        <h2>{{ computedFullName}}</h2>
    </div>
</template>

<script>
import {ref, reactive, toRefs, computed, watch} from 'vue'
    export default {
        name:'Methods',
        setup(){
            const count = ref(0)
            const name = ref('jeffrey')
            const state = reactive({
                first: 'Burce',
                last: 'Wayne'
            })
            // it also can be array, either one change, do the inspection
            watch([name], (newValue, oldValue)  =>  {
                console.log('newValue',newValue[0])
                console.log('oldValue',oldValue[0])
            },{
                immediate: true
            })
            
            // make it works on the reactive object
            watch(() => {
                return state.first
            }, (newValue, oldValue)  =>  {
                console.log('newValue',newValue)
                console.log('oldValue',oldValue)
            },{
                immediate: true,
                deep: true  // when the object has nested infomation
            })
            
            //  reactive object -> single 
            watch(() => {
                return {...state}
            }, (newValue, oldValue)  =>  {
                console.log('newValue',newValue)
                console.log('oldValue',oldValue)
            },{
                immediate: true
            })
            
            const computedFullName = computed(function() {
                return `${state.first} ${state.last}`
            })
            
            function IncreaseCount() {
                count.value ++;
            }
            function changeName(){
                state.first = 'Clark'
                state.last  = 'Kent'
            }
            
            return {
                count,
                name,
                IncreaseCount,
                ...toRefs(state),
                changeName,
                computedFullName
            }
        },
        data(){
            return {
            }
        }
    }
    
</script>

<style scoped>

</style>
```

```javascript
//first argment: props
// second argment: context
setup(props, context){
    
}
props: [['first']],
emits: ['callheros']
```

[Vue JS 3 Tutorial - 66 - Deploying Vue Applications - YouTube](https://www.youtube.com/watch?v=qduayAPJK9A&list=PLC3y8-rFHvwgeQIfSDtEGVvvSEPDkL_1f&index=66)
