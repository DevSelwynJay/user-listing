<template>
    <q-page>
        <q-page-sticky position="top-right" :offset="[18, 18]" style="z-index: 99;">
            <div class="row items-center q-gutter-sm">
            <q-btn to="/" label="Go to User View" @click="linkClick" color="primary" />
            </div>
        </q-page-sticky>
        <UserList />
    </q-page>
</template>
  
<script setup>
    import UserList from 'components/UserList.vue'

    defineOptions({
        name: 'AdminPage'
    });
</script>
  