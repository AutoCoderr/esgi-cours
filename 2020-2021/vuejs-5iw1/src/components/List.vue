<template>
  <div>
    <h1>List</h1>
    <button @click="alertCountComputed">computed</button>
    <button @click="alertCountMethod">method</button>
    <button @click="addItem">add item</button>
    {{ countList }} {{ countListMethod() }}
    <ul v-bind:style="listStyle">
      <li
        v-for="item in list"
        :key="item.id"
        v-html="$options.filters.ucfirst($options.filters.rInRed(item.name))"
      ></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "List",
  props: {
    listStyle: Object,
  },
  data: () => ({
    list: [{ id: 1, name: "Kakarl" }],
  }),
  methods: {
    addItem: function () {
      this.$data.list.push({
        id: Date.now(),
        name: `toto-${this.$data.list.length + 1}`,
      });
    },
    countListMethod: function () {
      console.error("count method");
      return this.$data.list.length;
    },
    alertCountComputed: function () {
      alert(this.countList);
    },
    alertCountMethod: function () {
      alert(this.countListMethod());
    },
  },
  created: () => console.log("created"),
  mounted: () => console.log("mounted"),
  updated: () => console.log("updated"),
  destroyed: () => console.error("destroyed"),
  computed: {
    countList: function () {
      console.error("count computed");
      return this.$data.list.length;
    },
  },
  filters: {
    ucfirst: function ucfirst(str) {
      if (typeof str !== "string" || str.length === 0) return "";
      return str[0].toUpperCase() + str.substring(1);
    },
    rInRed: (word) => {
      return word.replaceAll("r", '<span style="color: red;">r</span>');
    },
  },
};
</script>