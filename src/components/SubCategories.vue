<template>
  <div class="wrapper">
    <div class="categorySection">
      <div class="head">
        <div>Sub-Categories</div>
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
          v-for="subCategory in subCategoryList"
          :key="subCategory.id"
        >
          <div @click="getChilds(subCategory.id)">{{ subCategory.title }}</div>
        </div>
        <div v-if="addNewItem == true">
          <input type="text" v-model="newCategory.title" />
          <input type="submit" value="Add" @click="addCategory" />
        </div>
      </div>
    </div>
    <div v-if="childList !== null">
      <SubCategories :subCategoryList="childList" :parentId="categoryId" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HomeComponent",
  components: {
    SubCategories: () => import("@/components/SubCategories.vue"),
  },
  props: {
    subCategoryList: {
      type: Array,
    },
    parentId: {
      type: Number,
    },
  },
  data() {
    return {
      childList: null,
      categoryId: null,
      addNewItem: false,
      newCategory: {
        title: null,
        CategoryId: this.parentId,
        is_deleted: false,
      },
    };
  },
  methods: {
    getChilds(parentId) {
      this.categoryId = parentId;
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
        .then(this.subCategoryList.push(this.newCategory))
        .catch((err) =>
          console.log("message: ", err.message, "status: ", err.status)
        );
    },
  },
};
</script>
