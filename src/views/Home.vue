<template>
  <div class="wrapper">
    <div class="categorySection">
      <div class="head">
        <div>Categories</div>
        <div class="buttons">
          <button class="editButton">Edit</button>
          <button class="deleteButton">Delete</button>
          <button class="addButton" @click="addNewItem = !addNewItem">
            Add
          </button>
        </div>
      </div>

      <div class="menu">
        <div
          class="category"
          v-for="category in parentList"
          :key="category.id"
          :id="category.id"
        >
          <div @click="getChilds(category.id)">{{ category.title }}</div>
        </div>
        <div v-if="addNewItem == true">
          <input type="text" v-model="newCategory.title" />
          <input type="submit" value="Add" @click="addCategory" />
        </div>
      </div>
    </div>
    <div v-if="childList !== null">
      <SubCategories :subCategoryList="childList" :parentId="parentId" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SubCategories from "@/components/SubCategories.vue";
import axios from "axios";
export default {
  name: "Home",
  components: {
    SubCategories,
  },
  data() {
    return {
      parentList: null,
      childList: null,
      addNewItem: false,
      parentId: null,
      newCategory: {
        title: null,
        CategoryId: null,
        is_deleted: false,
      },
    };
  },
  methods: {
    getChilds(parentId) {
      this.parentId = parentId;
      axios
        .get(`http://localhost:3000/category/child/${parentId}`)
        .then((get_response) => {
          if (get_response?.status === 200) this.childList = get_response.data;
        })
        .catch((err) =>
          console.log("message: ", err.message, "status: ", err.status)
        );
    },
    addCategory() {
      this.addNewItem = !this.addNewItem;
      axios
        .post(`http://localhost:3000/category/create`, this.newCategory)
        .then(this.parentList.push(this.newCategory))
        .catch((err) =>
          console.log("message: ", err.message, "status: ", err.status)
        );
    },
  },

  beforeCreate() {
    axios
      .get(`http://localhost:3000/category/parent`)
      .then((get_response) => {
        if (get_response?.status === 200) this.parentList = get_response.data;
      })
      .catch((err) =>
        console.log("message: ", err.message, "status: ", err.status)
      );
  },
};
</script>
