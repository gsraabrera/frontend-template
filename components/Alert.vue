<template>
    <div>
      <Transition    
        enter-active-class="duration-300 ease-out"
        enter-from-class="transform opacity-0"
        enter-to-class="opacity-100"
        leave-active-class="duration-200 ease-in"
        leave-from-class="opacity-100"
        leave-to-class="transform opacity-0">
        <div v-if="alertOpen" class="text-white px-6 py-4 border-0 rounded relative mb-4 mt-20 w-80 " :class="alertColor">
    
        <span v-if="alert.type==='success'" class="inline-block w-5 h-5 mr-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
        </span>
        <span v-else class="inline-block w-5 h-5 mr-1">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
        </span>
        <span  class="inline-block align-middle mr-8" v-html="alertMessage">
          <!-- <b class="capitalize">pink!</b>  -->
         
        </span>
        <button class="absolute bg-transparent text-2xl font-semibold leading-none right-0 top-0 mt-4 mr-6 outline-none focus:outline-none" v-on:click="closeAlert()">
          <span>×</span>
        </button>
      </div>
    </Transition>
    <!-- <button @click="alertOpen = !alertOpen">test</button> -->
    </div>
    
    </template>
    
    <script>
    import { mapState, mapActions } from 'vuex'
    export default {
      name: "Alert",
      data() {
        return {
          alertOpen: false
        }
      },
      computed: {
        ...mapState({
          alert: state => state.alert
        }),
        },
        watch: {
        'alert.type' (newVal, oldVal) {
          if (newVal != null) {
            if (newVal === 'error') {
              this.alertMessage = this.alert.message
              this.alertColor = 'bg-red-500'
              this.alertOpen = true
            } else {
              this.alertMessage = this.alert.message
              this.alertColor = 'bg-green-500'
              this.alertOpen = true
            }
          }
          setTimeout(() => {
            this.clearAlert()
            this.alertOpen = false
          }, 3000)
        },
        $route (to, from) {
          this.clearAlert()
        }
      },
      methods: {
        
        closeAlert(){
          this.alertOpen = false
        },
        ...mapActions({
          clearAlert: 'alert/clear'
        }),
      },
      
        
    }
    </script>