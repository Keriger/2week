<template>
  <div class="container column">

    <form class="card card-w30" @submit.prevent="addBlock">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="typeBlock">
          <option
            v-for="option in typeBlockOptions"
            :key="option"
            :value="option.value"
          >
            {{ option.label }}
          </option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea v-model.trim="text" id="value" rows="3"></textarea>
      </div>

      <button :disabled="disabledAddBtn" class="btn primary">Добавить</button>
    </form>

    <div class="card card-w70">
      <h3 v-if="!resume.length">Добавьте первый блок, чтобы увидеть результат</h3>
      <component v-else
                 v-for="(item, idx) in resume" :key="idx"
                 :is="`resume-${Object.keys(item)[0]}`"
                 v-bind="item"
      >
      </component>
    </div>

  </div>

  <comment-block></comment-block>

</template>

<script>
import axios from 'axios'

import ResumeTitle from '@/components/resume/ResumeTitle'
import ResumeAvatar from '@/components/resume/ResumeAvatar'
import ResumeSubtitle from '@/components/resume/ResumeSubtitle'
import ResumeText from '@/components/resume/ResumeText'

import CommentBlock from '@/components/comments/CommentBlock'

export default {
  data () {
    return {
      resume: [],
      typeBlockOptions: [
        {
          value: 'title',
          label: 'Заголовок'
        },
        {
          value: 'subtitle',
          label: 'Подзаголовок'
        },
        {
          value: 'avatar',
          label: 'Аватар'
        },
        {
          value: 'text',
          label: 'Текст'
        }
      ],
      typeBlock: 'title',
      text: ''
    }
  },
  methods: {
    async addBlock () {
      const resumeData = {
        [this.typeBlock]: this.text
      }
      await axios.post('https://vue-width-http-f52c4-default-rtdb.firebaseio.com/resume.json/',
        resumeData
      )
      this.resume.push(resumeData)
      this.text = ''
      this.typeBlock = 'title'
    },
    async getResumeBlockContent () {
      const { data } = await axios.get('https://vue-width-http-f52c4-default-rtdb.firebaseio.com/resume.json')

      Object.keys(data).map((key, idx) => {
        this.resume.push(Object.values(data)[idx])
      })
    }
  },
  computed: {
    disabledAddBtn () {
      return this.text.length < 4
    }
  },
  mounted () {
    this.getResumeBlockContent()
  },
  components: {
    ResumeTitle,
    ResumeAvatar,
    ResumeSubtitle,
    ResumeText,
    CommentBlock
  }
}
</script>

<style>

</style>
