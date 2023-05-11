<template>
  <div class="home">
    <h1>Home</h1>
    <p>
      {{ name }}
      {{ age }}
    </p>
    <button @click="changeValue">Click Me</button>
    <p v-if="show"> You click me</p>

    <!-- using reactive -->
    <div>
      {{ person_one.name }}
      {{ person_one.age }}
    </div>
    <button @click="changeName">Change Name</button>

    <!-- using ref -->
    <div>
      {{ person_two.name }}
      {{ person_two.age }}
    </div>
    <button @click="refFun">Change Name</button>

    <div>
      <input type="text" v-model="search">
      <div v-for="name in filterName" :key="name">
        {{ name }}
      </div>
    </div>
    <Post :posts="posts"></Post>
  </div>

</template>

<script>
import Post from '../components/Post'
import { computed, reactive, ref } from 'vue';

export default {
  components: { Post },
  setup(){
    let name = ref('min khant');
    let age = 19;
    //if you want to change value that value must be reactive so use ref(value);
    let show = ref(false);
    let changeValue = ()=>{
      show.value = !show.value;
      name.value = 'Min Khant'
    }

    // using reactive 
    let person_one = reactive({name:"Maung Maung", age :30})

    let changeName = ()=>{
      // no need value when we use reactive instance of ref
      // but reactive can only work array and object
      // not work with premitive type
      person_one.name = "Aung Aung"
    }

        // using ref
        let person_two = ref({name:"Kyaw Maung", age :30})

    let refFun = ()=>{
      // need value to change name 
      // person_two.value = {name: "Kyaw Kyaw", age :30}
      person_two.value.name = "Kyaw Kyaw";
    }
 

    //test computed properties
    let search = ref(null);
    let names = ref(['aung aung', 'maung maung', 'su su', 'kyaw kyaw', 'aye aye'])
    let filterName = computed(()=>{
      return names.value.filter(name => name.includes(search.value))
    })

    //test post 
    let posts = ref([
      {id:1 , title : "post1", 
      body: "Lorem ipsum dolor, sit amet consectetur adipisicing elit. At temporibus, voluptatum vitae veniam officia mollitia impedit illum aut cumque? Enim voluptas omnis accusantium. Numquam nostrum quos voluptas aspernatur, at dictaLabore, quam! Mollitia fugit sint quae distinctio inventore velit dolorum natus maiores voluptatum corporis labore dolore doloribus quidem, illo eum sapiente cupiditate ipsam deleniti neque. Tempore ipsum possimus sit dolor.Debitis atque beatae placeat fuga, dolore ab animi facere impedit quod, inventore, nobis quasi iste facilis eveniet blanditiis. Repellendus accusantium molestias autem dignissimos voluptatum pariatur alias veniam qui velit cum"},
      {id:2 , title : "post2", body: "lorem"},
      {id:3 , title : "post3", body:"lorem"},
    ])

    //return when need to use in template
    return {
      name, age, show, changeValue, person_one,
      changeName,person_two,refFun, filterName, names, search, posts
    };
  }
}
</script>
