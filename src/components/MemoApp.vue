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
      @updateMemo="updateMemo"
      :editingId="editingId"
      @setEditingId="SET_EDITING_ID"
      @resetEditingId="RESET_EDITING_ID" />
    </ul>
  </div>
</template>
<script>
import MemoForm from './MemoForm'
import Memo from './Memo'

import axios from 'axios'
const memoAPICore = axios.create({
  baseURL: 'http://localhost:8000/api/memos'
})

import { mapActions, mapState, mapMutations } from 'vuex'
import { RESET_EDITING_ID, SET_EDITING_ID } from '../store/mutations-types'

export default {
  name: 'MemoApp',
  components: {
    MemoForm,
    Memo
  },
  data () {
    return {
    }
  },
  computed: {
    ...mapState([
      'memos',
      'editingId'
    ])
  },
  created () {
    this.fetchMemos()
  },
  methods: {
    ...mapActions([
      'fetchMemos',
      'addMemo',
      'deleteMemo',
      'updateMemo'
    ]),
    ...mapMutations([
      SET_EDITING_ID,
      RESET_EDITING_ID
    ])
  }
}
</script>
<style scoped>
  .memo-list {
    padding: 20px 0;
    margin: 0;
  }
</style>
