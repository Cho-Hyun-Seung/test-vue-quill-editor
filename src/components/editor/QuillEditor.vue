<template>
  <div class="editor-wrapper">
    <EditorActionBar/>
    <Toolbar/>
    <div class="editor-body">
      <!-- 조건 : 포커스 없고, 텍스트 없을 때만 placeholder 보이기 -->
      <div v-if="!isFocused && !hasText" class="custom-placeholder">
        내용을 입력해주세요.
      </div>
      <div ref="quillEditor" class="real-editor"></div>
    </div>
  </div>
</template>


<script>
import {ref, onMounted, nextTick} from 'vue'
import Quill from 'quill'
import 'quill/dist/quill.snow.css'
import QuillResize from 'quill-resize-module';
import Toolbar from './Toolbar.vue'
import EditorActionBar from './EditorActionBar.vue'

Quill.register('modules/resize', QuillResize);

export default {
  name: 'QuillEditor',
  components: {Toolbar, EditorActionBar},
  setup() {
    const quillEditor = ref(null)
    const isFocused = ref(false)
    const hasText = ref(false)

    onMounted(async () => {
      const quill = new Quill(quillEditor.value, {
        theme: 'snow',
        modules: {
          toolbar: {
            container: '#toolbar',
            handlers: {
              image: () => {
                console.log("이미지 핸들러 작동");
                const input = document.createElement('input');
                input.setAttribute('type', 'file');
                input.setAttribute('accept', 'image/*'); // TODO 이미지 타입 제한하기
                input.click();

                input.onchange = async () => {
                  console.log("onchange 작동");
                  const file = input.files[0];
                  if (file) {
                    console.log("파일 존재")
                    const reader = new FileReader();
                    reader.onload = (e) => {
                      const range = quill.getSelection(true);
                      quill.insertEmbed(range.index, 'image', e.target.result);

                      nextTick(() => {
                        const img = quill.root.querySelector(`img[src="${e.target.result}"]`);
                        if (img) {
                          img.setAttribute('width', '600'); // 초기에 300px 고정
                          img.style.height = '100%';
                        }
                      });
                    };
                    reader.readAsDataURL(file);
                  }
                }
              }
            }
          },
          /* https://github.com/mudoo/quill-resize-module */
          resize: {
            parchment: {
              image: {
                attribute: ['width'],  // ['width', 'height']
                limit: {
                  minWidth: 200,
                  maxWidth: 1000,
                  maxHeight: 1000,
                }
              }
            }
          }
        },
        placeholder: ' ',
      })

      quill.on('selection-change', (range) => {
        if (range) {
          isFocused.value = true
        } else {
          isFocused.value = false
        }
      })

      quill.on('text-change', () => {
        const content = quill.getText().trim()
        hasText.value = content.length > 0
      })
    })

    return {
      quillEditor,
      isFocused,
      hasText,
    }
  }
}
</script>


<style scoped>
.editor-wrapper {
  width: 100%;
  height: 100%;
  background: #fff;
  display: flex;
  flex-direction: column;
}

.editor-body {
  position: relative;
  flex-grow: 1;
  padding: 20px;
  overflow-y: auto;
  height: 100%;
}

.real-editor {
  min-height: 400px;
  border: none;
}

/* 커스텀 placeholder */
.custom-placeholder {
  position: absolute;
  top: 30px;
  left: 35px;
  color: #aaa;
  font-size: 14px;
  pointer-events: none;
  user-select: none;
  transition: opacity 0.3s ease;
  opacity: 1;
}

/* 사라지는 애니메이션은 v-if가 아니라 직접 opacity 조절해야 한다면 추가 */
</style>

