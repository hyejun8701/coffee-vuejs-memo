<template>
  <div class="memo-app">
    <memo-form @addMemo="addMemo" />
    <div>
      사용방법: 
      <ol>
        <li>내용을 더블클릭하면 input 으로 변경된다.</li>
        <li>input 에서 엔터를 치면 수정한 내용으로 변경되어 저장된다.</li>
        <li>마우스로 다른 곳을 클릭하면 수정한 내용으로 변경되지 않고, input 을 빠져나온다.</li>
        <li>오른쪽 상단 <i class="fas fa-times"></i> 버튼으로 삭제할 수 있다.</li>
      </ol>
    </div>
    <ul class="memo-list">
      <memo v-for="memo in memos"
      :key="memo.id"
      :memo="memo"
      @deleteMemo="deleteMemo"
      @updateMemo="updateMemo" />
    </ul>
  </div>
</template>
<script>
import MemoForm from './MemoForm'
import Memo from './Memo'
export default {
  name: 'MemoApp',
  components: {
    MemoForm,
    Memo
  },
  data () {
    return {
      memos: [],
    }
  },
  created () {
    this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : []
  },
  methods: {
    addMemo (payload) {
      this.memos.push(payload)
      this.storeMemo()
    },
    storeMemo () {
      const memoToString = JSON.stringify(this.memos)
      localStorage.setItem('memos', memoToString)
    },
    deleteMemo (id) {
      const targetIndex = this.memos.findIndex(v => v.id === id)
      this.memos.splice(targetIndex, 1)
      this.storeMemo()
    },
    updateMemo (payload) {
      const { id, content } = payload
      const targetIndex = this.memos.findIndex(v => v.id === id)
      const targetMemo = this.memos[targetIndex]
      console.log(...targetMemo)
      console.log(content)
      this.memos.splice(targetIndex, 1, { ...targetMemo, content })
      this.storeMemo()
    }
  }
}
</script>
<style scoped>
  .memo-list {
    padding: 20px 0;
    margin: 0;
  }
</style>
