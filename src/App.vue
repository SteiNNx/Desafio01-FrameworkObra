<template>
  <div id="app">
    <a-layout class="layout">
      <a-layout-header style="height: 10rem; display: flex; justify-content: center">
        <Navbar />
      </a-layout-header>
      <a-layout-content style="padding: 0 50px">
        <a-row type="flex">
          <a-col :span="24">
            <a-table :columns="columns" :data-source="data">
              <a slot="name" slot-scope="text">{{ text }}</a>
              <span slot="customTitle"><a-icon type="smile-o" /> Name</span>
              <span slot="tags" slot-scope="tags">
                <a-tag
                  v-for="tag in tags"
                  :key="tag"
                  :color="
                    tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'
                  "
                >
                  {{ tag.toUpperCase() }}
                </a-tag>
              </span>
              <span slot="action" slot-scope="text, record">
                <a>Invite 一 {{ record.name }}</a>
                <a-divider type="vertical" />
                <a>Delete</a>
                <a-divider type="vertical" />
                <a class="ant-dropdown-link"> More actions <a-icon type="down" /> </a>
              </span>
            </a-table>
          </a-col>

          <a-col :span="24">
            <a-button type="primary" @click="handleOnClickModal(true)"
              >Abrir Modal</a-button
            >
            <a-modal
              v-model="isOpenModal"
              title="Ejemplo Modal"
              @ok="handleOnClickModal(false)"
            >
            </a-modal>
          </a-col>
        </a-row>
      </a-layout-content>
      <a-layout-footer>Footer</a-layout-footer>
    </a-layout>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar";
const columns = [
  {
    dataIndex: "name",
    key: "name",
  },
  {
    dataIndex: "age",
    key: "age",
  },
  {
    dataIndex: "address",
    key: "address",
  },
  {
    key: "tags",
    dataIndex: "tags",
  },
];

const data = [
  {
    key: "1",
    name: "John Brown",
    age: 32,
    address: "New York No. 1 Lake Park",
    tags: ["nice", "developer"],
  },
  {
    key: "2",
    name: "Jim Green",
    age: 42,
    address: "London No. 1 Lake Park",
    tags: ["loser"],
  },
  {
    key: "3",
    name: "Joe Black",
    age: 32,
    address: "Sidney No. 1 Lake Park",
    tags: ["cool", "teacher"],
  },
];
export default {
  name: "App",
  components: {
    Navbar,
  },
  data() {
    return {
      isOpenModal: false,
      data,
      columns,
    };
  },
  methods: {
    handleOnClickModal(newStateIsOpenModal) {
      this.isOpenModal = newStateIsOpenModal;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
