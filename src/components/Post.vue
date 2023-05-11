<template>
    <h1>Post</h1>
    <div v-for="post in posts" :key="post.id">
        <SinglePost :post="post"></SinglePost>
    </div>
</template>

<script>
import { onMounted, onUnmounted } from 'vue'
import SinglePost from './SinglePost'
export default {
  components: { SinglePost },
        props : ['posts'],
        setup(props){
            // when we need to use props
            console.log(props.posts)
            onMounted(()=>console.log('component mounted'))
            onUnmounted(()=> console.log('component unmounted'));
        }
    }
</script>

<style scoped>

</style>