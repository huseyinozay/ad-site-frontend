<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: "Comic Sans MS", "Comic Sans", cursive;
  /* -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
  overflow-x: scroll;
}
.wrapper {
  display: flex;
}
.categorySection {
  margin: 10px;
  padding: 10px;
  height: 500px;
  width: 300px;
}
.menu {
  border: 3px solid;
  height: 400px;
  overflow-y: scroll;
}
.category {
  padding: 5px;
}
.category:hover {
  background-color: #95bcf2;
}
.head {
  display: flex;
  justify-content: space-between;
}
button {
  margin: 5px;
  font-family: "Comic Sans MS", "Comic Sans";
  box-shadow: 2px 2px;
  border: 2px;
}
.editButton {
  background-color: #95bcf2;
}
.deleteButton {
  background-color: #ea9999;
}
.addButton {
  background-color: #ffd966;
}
input[type="text"] {
  width: 200px;
  height: 20px;
  padding-right: 50px;
  border: 1px solid;
}
input[type="submit"] {
  margin-left: -62px;
  width: 60px;
  height: 20px;
  border: 0;
}
</style>
