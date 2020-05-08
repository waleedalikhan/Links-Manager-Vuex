<template>
  <div class="hello">
    <div class="left">
      <h1>{{ title }}</h1>
      <form @submit.prevent="addLink">
        <input type="text" class="link-input" placeholder="Add a link" v-model="newLink" />
      </form>
      <ul>
        <li v-for="link in links" :key="link.id">
          <a :href="link" target="_blank">{{ link }}</a>
          <button @click="removeLinks(link)" class="rm">Remove</button>
        </li>
      </ul>
    </div>
    <div class="right">
      <Stats />
    </div>
  </div>
</template>

<script>
import Stats from "./Stats.vue";
import { mapState, mapMutations, mapActions } from "vuex";

export default {
  data() {
    return {
      newLink: ""
    };
  },
  computed: {
    ...mapState(["title", "links"])
  },
  methods: {
    ...mapMutations(["ADD_LINK"]),
    ...mapActions(["removeLink"]),
    addLink() {
      this.ADD_LINK(this.newLink);
      this.newLink = "";
    },
    removeLinks: function(link) {
      // Add this
      this.removeLink(link);
    }
  },
  components: {
    Stats
  }
};
</script>

<style>
html,
#app,
.home {
  height: 100%;
}
body {
  background-color: #f4f4f4;
  margin: 0;
  height: 100%;
}

.hello {
  display: grid;
  grid-template-columns: repeat(2, 50%);
  grid-template-rows: 100%;
  grid-template-areas: "left right";
  height: 100%;
}

.left,
.right {
  padding: 30px;
}

ul {
  list-style-type: none;
  padding: 0;
}
ul li {
  padding: 20px;
  background: white;
  margin-bottom: 8px;
}

.right {
  grid-area: right;
  background-color: #e9e9e9;
}

input {
  border: none;
  padding: 20px;
  width: calc(100% - 40px);
  box-shadow: 0 5px 5px lightgrey;
  margin-bottom: 50px;
  outline: none;
}
.rm {
  float: right;
  text-transform: uppercase;
  font-size: 0.8rem;
  background: #f9d0e3;
  border: 0;
  padding: 0.5rem;
  color: #ff0076;
  cursor: pointer;
}
</style>