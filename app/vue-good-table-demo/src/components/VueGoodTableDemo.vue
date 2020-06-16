<template>
  <div class="demo">
    <VueGoodTable
      :columns="columns"
      :rows="rows"
      :search-options="{
    enabled: true,
    skipDiacritics: true,
    placeholder: 'Search this table',
  }"
    />
  </div>
</template>

<script>
import { VueGoodTable } from "vue-good-table";
import "vue-good-table/dist/vue-good-table.css";

export default {
  name: "VueGoodTableDemo",
  components: {
    VueGoodTable
  },
  data() {
    return {
      rows: [
        {
          id: 1,
          name: "John",
          age: 20,
          createdAt: "",
          score: 0.03343
        },
        {
          id: 2,
          name: "Jane",
          age: 24,
          createdAt: "2011-10-31",
          score: 0.03343
        },
        {
          id: 3,
          name: "Susan",
          age: 16,
          createdAt: "2011-10-30",
          score: 0.3342
        },
        {
          id: 4,
          name: "Chris",
          age: 55,
          createdAt: "2011-10-11",
          score: 0.41571
        },
        {
          id: 5,
          name: "Dan",
          age: 40,
          createdAt: "2011-10-21",
          score: 0.9045
        },
        {
          id: 6,
          name: "John",
          age: 20,
          createdAt: "2011-10-31",
          score: 0.02901
        }
      ]
    };
  },
  computed: {
    columns() {
      return [
        {
          label: "Name",
          field: "name",
          filterOptions: {
            enabled: true,
            placeholder: "All",
            filterDropdownItems: this.getDropdownItems("name")
          }
        },
        {
          label: "Age",
          field: "age",
          type: "number",
          filterOptions: {
            enabled: true,
            placeholder: "All",
            filterDropdownItems: this.getDropdownItems("age")
          }
        },
        {
          label: "Created On",
          field: "createdAt",
          type: "date",
          dateInputFormat: "yyyy-MM-dd",
          dateOutputFormat: "MMM Do yy",
          filterOptions: {
            enabled: true,
            placeholder: "All",
            filterDropdownItems: this.getDropdownItems("createdAt")
          }
        },
        {
          label: "Percent",
          field: "score",
          type: "percentage",
          filterOptions: {
            enabled: true,
            placeholder: "All",
            filterDropdownItems: this.getDropdownItems("score")
          }
        }
      ];
    }
  },
  methods: {
    getDropdownItems(property) {
      const array = Array.from(
        new Set(this.rows.map(obj => obj[property]).sort())
      );

      if (property === "score") {
        return array.map(value => {
          return { value: value, text: this.formatScore(value) };
        });
      } else {
        return array;
      }
    },
    formatScore(score) {
      return (score * 100).toFixed(2) + "%";
    }
  }
};
</script>
