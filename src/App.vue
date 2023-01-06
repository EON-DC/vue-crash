<template>
  <div class="container">
    <ol class="list-group list-group-numbered">
      <li v-for="grammar in data.grammars" v-bind:key="grammar" class="list-group-item d-flex justify-content-between align-items-start">
        <div class="ms-2 me-auto">
          <div class="fw-bold">{{ grammar.word }}</div>
          {{ grammar.meaning }}
        </div>
        <span class="badge bg-primary rounded-pill">14</span>
      </li>
      <li v-if="data.grammars.length == 0" class="list-group-item d-flex justify-content-between align-items-start">
        <div class="ms-2 me-auto">
          <div class="fw-bold">게시물이 없습니다</div>
          <span>저장된 게시물이 없습니다.</span>
        </div>
        <span class="badge bg-primary rounded-pill">0</span>
      </li>
    </ol>
  </div>
</template>

<script>
import { reactive, onMounted } from "vue";

export default {
  name: "App",
  methods: {},
  components: {},

  setup() {
    const data = reactive({
      grammars: [],
    });
    // 게시판 API를 호출해서 전달
    const getList = () => {
      fetch("http://localhost:9000/api/grammars")
        .then((response) => response.json())
        .then((response) => {
          data.grammars = response;
        });
    };

    onMounted(() => {
      getList();
      console.log(getList);
    });
    return {
      data: data,
      getList: getList,
    };
  },
};
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css";
</style>
