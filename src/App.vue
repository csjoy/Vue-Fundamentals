<script setup lang="ts">
const color = "red"
const isUppercase = true
const msg = "My message"
const logo = "/vite.svg"
const count = 7
const html = `Stylise</br>HTML in<br/><b>your data</b>`
const link = {
  title: "Go to Google",
  url: "https://google.com",
  tabindex: 1,
  target: "_black",
}

const interests = ["TV", "Games", "Sports"]
const items = [
  {
    id: 1,
    title: "Item 1",
    description: "About item 1",
    characteristics: ["Summer", "Winter", "Spring", "Autumn"]
  },
  {
    id: 2,
    title: "Item 2",
    description: "About item 2",
    characteristics: ["North", "West", "East", "South"]
  }
]

const interestsObject = [
  {
    title: "TV",
    favorites: ["Designated Survivor", "Spongebob"],
  },
  {
    title: "Games",
    favorites: ["CS:GO"],
  },
  {
    title: "Sports",
    favorites: [],
  }
]

const course = {
  title: "Frontend development with Vue",
  description: "Learn the awesome of Vue",
  lecturer: "Maya and Raymond",
}

const information = {
  title: "My list component information",
  subtitle: "Vue JS basics",
  items: ["Looping", "Data", "Methods"],
}

const myMethod = () => {
  console.log("my first method")
}

const triggerAlert = (index: number) => {
  alert(`${index} has been clicked`)
}


</script>

<template>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
  <p>{{ isUppercase ? color.toUpperCase() : color }}</p>
  <div v-text="msg"></div>
  <div>{{ msg }}</div>
  <img :src="logo" alt="logo">
  <div v-if="count === 2">Two</div>
  <div v-else-if="count === 4">Four</div>
  <div v-else-if="count === 6">Six</div>
  <div v-else>Other</div>
  <div>
    <h1 v-html="html"></h1>
  </div>
  <a :href="link.url" :target="link.target" :tabindex="link.tabindex">{{ link.title }}</a>
  <div class="form">
    <label>Name
      <input type="text" v-model="name" placeholder="enter here" class="border-gray-500 border bg-gray-50 rounded">
    </label>
    <label>
      Preferred JavaScript style
      <select name="language" v-model="language">
        <option value="JavaScript">JavaScript</option>
        <option value="TypeScript">TypeScript</option>
        <option value="CoffeeScript">CoffeeScript</option>
        <option value="Dart">Dart</option>
      </select>
    </label>
  </div>
  <ul class="overview">
    <li>
      <string>Overview</string>
    </li>
    <li>Name: {{ name }}</li>
    <li>Preference: {{ language }}</li>
  </ul>


  <div v-for="n in 5" :key="`loop-1-${n}`">{{ n }}</div>
  <h1>Looping through arrays</h1>
  <ul>
    <li v-for="(item, index) in interests" :key="index">{{ item }}</li>
  </ul>

  <ul>
    <li v-for="item in items" :key="item.id">
      <h2>{{ item.title }}</h2>
      <span>{{ item.description }}</span>
      <ul>
        <li v-for="(str, index) in item.characteristics" :key="index">
          <span>{{ str }}</span>
        </li>
      </ul>
    </li>
  </ul>

  <h2 class="text-2xl font-semibold">Looping through array of objects</h2>
  <ul class="p-4">
    <li v-for="(interest, index) in interestsObject" :key="index" class="my-4 rounded-lg bg-gray-100 max-w-md p-4">{{ interest.title }}
      <ol v-if="interest.favorites.length > 0">
        <li v-for="(fav, idx) in interest.favorites" :key="idx">{{ `${idx + 1}. ${fav}` }}</li>
      </ol>
    </li>
  </ul>

  <h2 class="text-2xl font-semibold">Iterating through a keyed collection (Object)</h2>
  <ul>
    <li v-for="(value, key, index) in course" :key="index">
      {{ index }}. {{ key }}: {{ value }}</li>
  </ul>

  <div>
    <div v-for="(value, key) in information" :key="key">{{ key }}: {{ value.toString() }}</div>
  </div>

  <button v-on:click="myMethod">Click me</button>
  <button @click="myMethod">Click Here</button>

  <div>
    <h2 class="text-2xl font-semibold">Triggering Vue Methods</h2>
    <ul>
      <li v-for="index in 5" :key="index" class="p-2">
        <button @click="triggerAlert(index)" class="px-5 py-2.5 bg-gray-100 rounded-lg">Trigger {{ index }}</button>
      </li>
    </ul>
  </div>

  <div>
    <h2 class="text-2xl font-semibold">Returning Methods</h2>
    <div>Cart ({{ totalItems }}) {{ formatCurrency(totalCost) }}</div>
    <ul class="p-4">
      <li v-for="n in 5" :key="n">
        <button @click="addToCart(n)" class="px-5 py-2.5 bg-gray-100 rounded-lg my-4">Add {{ formatCurrency(n) }}</button>
      </li>
    </ul>
  </div>

  <div class="container">
    <h1 class="text-2xl font-semibold">Vue Lifecycle hooks</h1>
    <ul>
      <li v-for="(item, index) in list" :key="index">
        {{ item }}
        <button class="px-5 py-2.5 bg-gray-200 rounded-lg" @click="deleteItem(item)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      totalCost: 0,
      totalItems: 0,
      name: "",
      language: "",
      list: [
        "Apex Legends",
        "A Plague Tale: Innocence",
        "ART SQOOL",
        "Baba Is You",
        "Devil May Cry 5",
        "The Division 2",
        "Hypnospace Outlaw",
        "Katana ZERO",
        "testing unmounted hooks"
      ]
    }
  },
  beforeCreate() {
    alert("beforeCreate: data is static, that's it")
  },
  created() {
    alert("created: data and events ready, but no DOM")
  },
  beforeMount() {
    alert("beforeMount: element not ready")
  },
  mounted() {
    alert("mounted: DOM ready to use")
  },
  beforeUpdate() {
    alert("beforeUpdate: we know an update is about to happen, and have the data")
  },
  updated() {
    alert("updated: virtual DOM will update after you click OK")
  },
  beforeUnmount() {
    alert("beforeUnmount: about to blow up this components")
  },
  unmounted() {
    alert("unmounted: this component has been destroyed")
  },
  methods: {
    addToCart(n: number) {
      this.totalItems = this.totalItems + 1
      this.totalCost = this.totalCost + n
    },
    formatCurrency(val: number) {
      return `$${val.toFixed(2)}`
    },
    deleteItem(value: string) {
      this.list = this.list.filter(item => item !== value)
    }
  },
}

</script>