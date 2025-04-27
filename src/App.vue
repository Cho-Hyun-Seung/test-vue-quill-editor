<template>
  <div id="app">
    <div class="editor-container">
      <QuillEditor />
    </div>
  </div>
</template>

<script>
import { QuillEditor } from './components/Editor'

export default {
  name: 'App',
  components: {
    QuillEditor
  }
}
</script>

<style scoped>
#app {
  width: 100vw;
  min-height: 100vh;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center; /* 가운데 정렬 */
  align-items: flex-start; /* 위에서부터 시작 */
  background: #f9f9f9;
  overflow-x: hidden;
}

.editor-container {
  max-width: 1500px; /* 에디터 최대 폭 제한 */
  min-width: 700px;
  margin-top: 50px; /* 위 여백 */
  background: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1); /* 약간 그림자 */
  border-radius: 8px; /* 모서리 둥글게 */
  overflow: hidden;
}
</style>
