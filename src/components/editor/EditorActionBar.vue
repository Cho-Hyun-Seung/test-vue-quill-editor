<template>
  <div id="action-bar">
    <button>📷 사진</button>
    <button>🎥 동영상</button>
    <button>📁 파일</button>
    <button>🗺️ 지도</button>
    <button>🗳️ 투표</button>
    <button>🔗 HTML</button>
  </div>
</template>

<script>
export default {
  name: 'EditorActionBar'
}
</script>

<style scoped>
#action-bar {
  display: flex;
  gap: 12px;
  background: #fafafa;
  padding: 8px 16px;
  border-bottom: 1px solid #ddd;
}
button {
  background: none;
  border: none;
  font-size: 14px;
  cursor: pointer;
}
</style>
