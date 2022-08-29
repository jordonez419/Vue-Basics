<template>
<div class="home">
  <div>
    <h1>{{counterTitle}}</h1>
    <h3>{{counterData.title}}</h3>
    dsads
      <button @click = "decreaseCounter(2,$event)" class="btn">--</button>
      <button @click = "decreaseCounter(1,$event)" class="btn">-</button>
      <span class="counter">{{counterData.count}}</span>
      <button @click = "increaseCounter(1,$event)" class="btn">+</button>
      <button @click = "increaseCounter(2,$event)" class="btn">++</button>
  </div>
  <p>This counter is {{oddOrEven}}</p>
  <div class="edit">
    <h4>Edit Counter Title</h4>
    <input v-model="counterData.title" type="text" placeholder="Type to change header">
  </div>
</div>
</template>
<!-- Script Set up Pattern Below. This is the best pattern to use!!  -->

<script setup>
    // With the script set up patter, we don't need to return any of our variables or methods
    import {ref, reactive, computed, watch, onBeforeMount, onMounted, onUnmounted, onBeforeUnmount} from 'vue'
    // const counter = ref(0)
    // To create a non-Reactive piece of data, simply declare it as a variable without the ref() vue method
    const counterTitle = 'Counter App'



    const counterData = reactive({
      // Inside of this reactive object, we are storing related data properties in the effort to group relevant code together.
      count:0,
      title: 'Counter'
    })

  // This is a watcher, a watcher is Vue function that 'watches for
  // certain data to change, it then fires off some code when the change occurs
  // Within the Watch hook, we need a 'getter' function to retrieve the
  // data from within our reactive object, thats why we have a function
  // inside of the watch function itself
    watch(()=> counterData.count, (newCount) =>{
      console.log('new count:', newCount)
      if (newCount == 20){
        alert('you hit 20')
      }
    })

    const oddOrEven = computed(() =>{
      if(counterData.count % 2 == 0){
        return 'Even'
      }
      else{
        return 'Odd'
      }
    })

    const increaseCounter = (num,e) =>{
      // When you create a ref variable, under the hood an object is being made. 
      // In order to access the value of that ref variable, use dot notation and fetch the 'value' property in the ref object
      counterData.count += num
      console.log(e)
    }

    const decreaseCounter = (num,e)=>{ 
      if(counterData.count == 0 ){
        return
      }
      counterData.count -= num
      console.log(e)
    }
    // Lifecycle Hooks below
    onBeforeMount(() =>{
      // This hook will fire off its code BEFORE the component is mounted
      console.log('on before mount')
    })
    onMounted(() =>{
      // This hook fires off its code once a component mounts (loads in the browser)
      console.log('on Mounted')
    })
    onBeforeUnmount(() =>{
      // This hook fires off its code right before the component unmounts
      console.log('on beforeUnmount')
    })
    onUnmounted(() =>{
      // This hook fires off its code once the component is fully unMounted
      console.log('on UnMounted')
    })
</script>


<style scoped>
.home{
  text-align: center;
  padding: 1rem;
}
.btn, .counter{
font-size: 40px;
margin:1rem
}
.edit{
  margin-top: 1rem;
}
</style>


<!--
<script>
// Options API Version below
// export default{
//   data(){
//     return {
//       counter: 0
//     }
//   },
// name:'Home',
// methods:{
//   increaseCounter(){
//   this.counter++
// },
// decreaseCounter()
// {
//   if(this.counter == 0){
//     return
//   }
//   this.counter--
// }
// }
// }

// composition API Version Below (Set up function pattern. Original pattern but not as good as the new pattern)
import {ref} from 'vue'

// export default{
//   setup(){
//     const counter = ref(0)

//     const increaseCounter = () =>{
//       // When you create a ref variable, under the hood an object is being made. 
//       // In order to access the value of that ref variable, use dot notation and fetch the 'value' property in the ref object
//       counter.value++
//     }

//     const decreaseCounter = ()=>{
//       if(counter.value == 0 ){
//         return
//       }
//       counter.value--
//     }

//     return{
//       // return statement should always be at the bottom of set up function
//       // Down here you will return any variables and methods
//       counter,
//       increaseCounter,
//       decreaseCounter
//     }
//   }
// }

</script> -->
