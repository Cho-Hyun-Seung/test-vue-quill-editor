<template>
  <div id="toolbar">
    <span class="ql-formats">
      <select class="ql-font">
        <option value="default">기본서체</option>
        <option value="serif">명조체</option>
        <option value="monospace">모노스페이스</option>
      </select>

      <select class="ql-size">
        <option value="small">12</option>
        <option selected>14</option>
        <option value="large">18</option>
        <option value="huge">24</option>
      </select>
    </span>

    <span class="ql-formats">
      <button class="ql-bold" title="굵게"></button>
      <button class="ql-italic" title="기울임꼴"></button>
      <button class="ql-underline" title="밑줄"></button>
    </span>

    <span class="ql-formats">
      <button class="ql-image" title="이미지 삽입"></button>
      <button class="ql-link" title="링크 삽입"></button>
    </span>
  </div>
</template>

<script>
export default {
  name: 'Toolbar'
}
</script>

<style scoped>
#toolbar {
  display: flex;
  gap: 12px;
  padding: 8px 16px;
  border-bottom: 1px solid #ddd;
  background: #fff;
}
select, button {
  background: none;
  border: none;
  font-size: 14px;
  cursor: pointer;
}
</style>
