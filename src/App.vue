<template>
  <div>
    <div class="alert-div">
      <app-alert :alert="alert" @close="alert = null" />
    </div>
    <div class="container column">
      <app-form @block-added="addBlock" />
      <app-resume
        :blocks="blocks"
        :loadingBlocks="loadingBlocks"
        @removeBlock="removeBlock"
      />
    </div>
    <div class="container">
      <app-comments-list
        :comments="comments"
        @load="loadComments"
        :loadingComments="loadingComments"
      />
    </div>
  </div>
</template>

<script>
import AppCommentsList from './components/AppCommentsList.vue';
import axios from 'axios';
import AppForm from './components/AppForm.vue';
import AppAlert from './components/AppAlert.vue';
import AppResume from './components/AppResume.vue';

export default {
  components: {
    AppCommentsList,
    AppForm,
    AppAlert,
    AppResume,
  },
  data() {
    return {
      blocks: [],
      comments: [],
      alert: null,
      loadingComments: false,
      loadingBlocks: false,
    };
  },
  created() {
    this.loadBlocks();
  },
  methods: {
    async loadComments() {
      try {
        this.loadingComments = true;
        const { data } = await axios.get(
          'https://jsonplaceholder.typicode.com/comments?_limit=42',
        );
        if (!data) {
          throw new Error('Список комментариев пуст');
        }
        this.comments = Object.keys(data).map((key) => {
          return {
            id: key,
            ...data[key],
          };
        });
        this.loadingComments = false;
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message,
        };
        this.loadingComments = false;
        console.log(e.message);
      }
    },
    async addBlock(block) {
      const response = await fetch(
        'https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks.json',
        {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            type: block.type,
            value: block.value,
          }),
        },
      );
      const firebaseData = await response.json();
      this.blocks.push({
        blockType: block.type,
        blockValue: block.value,
        id: firebaseData.value,
      });
      this.loadBlocks();
    },
    async loadBlocks() {
      try {
        this.loadingBlocks = true;
        const { data } = await axios.get(
          'https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks.json',
        );
        if (!data) {
          throw new Error('Список блоков пуст');
        }
        this.blocks = Object.keys(data).map((key) => {
          return {
            id: key,
            ...data[key],
          };
        });
        this.loadingBlocks = false;
      } catch (e) {
        this.alert = {
          type: 'danger',
          title: 'Ошибка!',
          text: e.message,
        };
        this.loadingBlocks = false;
      }
    },
    async removeBlock(id) {
      try {
        await axios.delete(
          `https://vue-resume-base-14cc9-default-rtdb.firebaseio.com/blocks/${id}.json`,
        );
        this.blocks = this.blocks.filter((block) => block.id !== id);
        this.alert = {
          type: 'primary',
          title: 'Успешно!',
          text: `Block с id:"${id}" был удалён`,
        };
      } catch (e) {
        console.log(e.message);
      }
    },
  },
};
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
  justify-content: center;
}
</style>
