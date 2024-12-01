<template>
<div>
  <div class="alert-div">
  <app-alert :alert="alert" @close="alert = null"></app-alert>
  </div>
  <div class="container column">
    <app-form
    @block-added="addBlock"
    ></app-form>
    <app-resume 
    :blocks="blocks" 
    :loadingBlocks="loadingBlocks"
    @remove2="removeBlock"
    ></app-resume>
  </div>
  <div class="container">
    <app-comments-list
    :emails="emails"
    :was-loaded="wasLoaded"
    @load="loadEmails"
    ></app-comments-list>
    <app-loader v-if="loading"></app-loader>
  </div>
</div>
</template>

<script>
/* eslint-disable */
import AppCommentsList from './components/AppCommentsList.vue';
import AppLoader from './components/AppLoader.vue';
import axios from 'axios'
import AppForm from './components/AppForm.vue';
import AppAlert from './components/AppAlert.vue';
import AppResume from './components/AppResume.vue';

export default {
  data() {
    return {
      emails: [],
      loading: false,
      wasLoaded: false,
      alert: null,
      blocks: [],
      loadingBlocks: false
    }
  },
  mounted () {
    this.loadBlocks()
  },
  methods: {
    async loadEmails () {
      try {
        this.loading = true
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        if (!data) {
          throw new Error('Список комментариев пуст') 
        }
        this.emails = Object.keys(data).map(key => {
          return {
            id: key,
            ...data[key]
          }
        }) 
        this.loading = false
        this.wasLoaded = true
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message
        }
        this.loading = false
        console.log(e.message)
      }
    },
    // addBlock(block) {
    //   this.blocks.push(block)
    // },
    async addBlock (block) {
      const response = await fetch('https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          type: block.type,
          value: block.value,
        })
      })
      const firebaseData = await response.json()
      this.blocks.push({
        blockType: block.type,
        blockValue: block.value,
        id: firebaseData.value
      })
      this.loadBlocks()
    },
    async loadBlocks () {
      try {
        this.loadingBlocks = true 
        const { data } = await axios.get('https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks.json')
        if (!data) {
          throw new Error('Список блоков пуст')
        }
        this.blocks = Object.keys(data).map(key => {
          return {
            id: key,
            ...data[key]
          }
        }) 
        this.loadingBlocks = false
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message
        }
        this.loadingBlocks = false
      }
    },
    async removeBlock (id) {
      try {
        await axios.delete(`https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks/${id}.json`)
        this.blocks = this.blocks.filter(block => block.id !== id)
        this.alert = {
          type: 'primary',
          title: 'Успешно!',
          text: `Block с id:"${id}" был удалён`
        }
      } catch (e) {
        console.log(e.message)
      }
    }
  },
  components: {
    AppLoader, AppCommentsList, AppForm, AppAlert, AppResume
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }

  .alert-div {
    display: flex; 
    justify-content: center
  }
</style>

<!-- // npm install axios --force -->
