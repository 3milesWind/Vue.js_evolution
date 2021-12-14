# Vue.js_evolution

## Create a simple project

1. yarn global add @vue/cli

2. vue create hello-world

3. cd hello-world

4. yarn serve

## Project Structure

1. A *.Vue file is a custom file formatr that uses HTML-Like syntax to describe a portion of the UI

2. Each *.Vue file consists of tree types of top-level language blocks
   
   1. <template></template>
   
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

* Two ways to blinding Textjavascript
  
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

Through the `v-bind` to add some arrtibutes to the html

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

* without keys, Vue uses an algorithm that minimuzes element movement and tries to patch/reuse elements of the same type in place as much as possible 

* Not using keys is only suitable when your list render output does not repy on temporary Dom state or child component state

* Althgough the default behavior of patching is more efficient, it can lead to problems

* a typpical value to provide to the key attribute is the id property is an Object. But any unique property will do as long as its not non-primitive value like Object or arrays

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

5. Contional List Rendering
   
   note that `v-for`can not write with `v-if` in the same line. `v-if`has the higher priority
   
   ```javascript
    <template v-for="name in names" :key="name">
       <h2 v-if="name === 'Bruce'"> {{name}}</h2>
     </template>
   ```
