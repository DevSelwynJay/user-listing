<template>
    <section class="userlist-section">
      <div class="userlist-container">
        <div class="text-h4 q-pb-md">Users</div>
        <div class="userlist-row">
          <template v-if="users.length > 0">
            <div v-for="user in users" :key="user.id" class="userlist-card" @click="showUserDetails(user)">
              <figure>
                <img src="https://randomuser.me/api/portraits/men/1.jpg">
              </figure>
              <dl>
                <h6>{{ user.firstName }} {{ user.lastName }}</h6>
                <p><q-icon name="phone" /> {{ user.mobileNumber }}</p>
              </dl>
            </div>
          </template>
          <template v-else>
            <div class="no-data-block">
              <div class="text-h2 q-mb-lg text-weight-bold">(='X'=)</div>
              <div class="text-h5">No data yet.</div>
            </div>
          </template>
        </div>
      </div>
      <q-dialog v-model="showDialog">
        <q-card>
          <q-card-section>
            <div class="text-h4 q-pb-sm">{{ selectedUser.firstName }} {{ selectedUser.lastName }}</div>
            <div class="text-subtitle1"><q-icon name="phone" /> {{ selectedUser.mobileNumber }}</div>
            <div class="text-subtitle1"><q-icon name="room" /> {{ selectedUser.address }}</div>
            <div class="text-subtitle1"><q-icon name="event" /> {{ selectedUser.date }}</div>
          </q-card-section>
          <q-card-actions align="right">
            <q-btn label="Close" color="primary" @click="closeDialog"/>
          </q-card-actions>
        </q-card>
      </q-dialog>
    </section>
  </template>
  
<script setup>
  import { ref } from 'vue'
  
  defineOptions({
    name: 'UserList'
  })

  const savedSubmissions = localStorage.getItem('submissions')
  const users = JSON.parse(savedSubmissions) ? JSON.parse(savedSubmissions) : []
  
  const showDialog = ref(false)
  const selectedUser = ref(null)
  
  const showUserDetails = (user) => {
    selectedUser.value = user
    showDialog.value = true
  }

  const closeDialog = () => {
    selectedUser.value = null
    showDialog.value = false
  }
</script>
  

<style lang="scss">
    .userlist-section{
        padding: 100px 1rem;
        height: 100vh;
        width: 100%;
        background: #FFFFFF;
        background: linear-gradient(135deg, #FFFFFF, #DADFE5);
    }
    .userlist-section .no-data-block{
      grid-column: 1 / -1;
      padding: 4rem 2rem;
      border-radius: 8px;
      text-align: center;
    }
    .userlist-container {
        max-width: 1200px;
        margin: 0 auto;
    }
    .userlist-container h4{
        font-weight: 600;
    }
    .userlist-row {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 24px;
        @media(max-width: 1024px){
          grid-template-columns: repeat(2, 1fr);
        }
        @media(max-width: 768px){
          grid-template-columns: repeat(1, 1fr);
        }
    }
    .userlist-card{
        border-radius: 8px;
        padding: 2rem 2rem;
        display: flex;
        gap: 1rem;
        align-items: center;
        cursor: pointer;
        transition: all ease 400ms;
        border: 1px solid $blue-grey-2;

        &:hover{
            box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
        }
    }
    .userlist-card figure{
        flex: none;
        margin: 0;
    }
    .userlist-card figure img{
        width: 100px;
        height: 100px;
        border-radius: 100%;
    }
    .userlist-card dl{
        margin: 0;
    }
    .userlist-card h6{
        margin: 0;
        font-weight: 600;
    }
    .userlist-card p{
        margin: 0;
    }
</style>