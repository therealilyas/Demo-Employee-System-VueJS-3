<template>
  <div class="app">
    <add-form @addEmp="addEmployee" />
    <all-employees @removeEmp="removeEmployee" :employees="employees" />
    <search-form @emtResults="emtResults" :employees="employees" />
    <edit-form v-if="!!edit" @editEmp="editEmployee" :results="results" />
  </div>
</template>

<script>
import AddForm from "./components/AddForm.vue";
import AllEmployees from "./components/AllEmployees.vue";
import SearchForm from "./components/SearchForm.vue";
import EditForm from "./components/EditForm.vue";

export default {
  name: "App",
  components: {
    AddForm,
    AllEmployees,
    SearchForm,
    EditForm,
  },
  created: function () {
    this.employees = [];
    this.results = {};
  },
  data() {
    return {
      employees: [],
      results: {},
      edit: false,
    };
  },
  methods: {
    addEmployee(employee) {
      employee.id = this.employees.length;
      employee.show = false;
      employee.showLessIcon = "";
      this.employees.push(employee);
    },
    removeEmployee(index) {
      delete this.employees[index];
      this.employees = this.employees.filter((employee) => !!employee);
    },
    emtResults(emp) {
      this.results = emp;
      this.edit = true;
    },
    editEmployee(emp) {
      for (let i; i < this.employees.length; i++) {
        if (emp.id == this.employees[i].id) {
          this.employees[i] = emp;
        } else {
          return;
        }
      }
      this.edit = false;
    },
  },
};
</script>
<style >
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.app {
  display: flex;
  height: 100%;
  max-width: 90%;
  padding: 5%;
  margin: 0 2.5%;
}
</style>