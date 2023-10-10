<template>
<section>
    <h1 v-if="prop.data" style="text-align:center">Edit this task</h1>
  <div class="container pt-5 h-100 d-flex justify-content-center align-items-center">
    <div class="card rounded-3" style="width: 60vw;">
        <form class="p-3" @submit.prevent="submitForm">
            <!-- Task input -->
            <div class="mb-4" :class="{err: nameError}" >
                <label class="form-label" for="form4Example1">Task Name</label>
                <input 
                    type="text" 
                    id="form4Example1" 
                    class="form-control" 
                    v-model="name"
                    @blur="validateField('name')"
                />
            </div>

            <!-- Task Desc input -->
            <div class="mb-4" :class="{err: descriptionError}" >
                <label class="form-label" for="form4Example3">Write a small description...</label>
                <textarea 
                    class="form-control" 
                    id="form4Example3" 
                    rows="2" 
                    v-model="description"
                    @blur="validateField('desc')"
                ></textarea>
            </div>

            <!-- Submit button -->
            <button type="submit" class="btn btn-primary">{{data ? 'Update' : 'Add'}}</button>
        </form>
    </div>
    </div>
    </section>
</template>

<script setup>
    import { ref, defineEmits, defineProps, onMounted } from "vue"
    import { toast } from 'vue3-toastify';
    import 'vue3-toastify/dist/index.css';
    const name = ref('')
    const description = ref('')
    const nameError = ref('');
    const descriptionError = ref('');
    const emit = defineEmits(['updated','add'])
    const prop = defineProps({
        data: Object
    })

    const notify = (params) => {
      toast(params, {
        autoClose: 1000,
      }); // ToastOptions
    }
    onMounted(() => {
        if(prop.data){ 
            name.value = prop.data.name,
            description.value = prop.data.desc
        }
    })

    const validateField = (param) => {
    let isValid = true
    if(param == 'name'){
        if (!name.value.trim()) {
            nameError.value = 'Name is required';
            isValid = false;
        } else {
            nameError.value = '';
        }
        return isValid
    }else {
        if (!description.value.trim()) {
            descriptionError.value = 'Description is required';
            isValid = false;
        } else {
            descriptionError.value = '';
        }
        return isValid;
        }
    }

    const validateForm = () => {
        let isValid = true;
        // Validate name presence
        isValid = validateField('name')

        // Validate description presence
        isValid = validateField('desc')
        return isValid
    }
    const submitForm = () => {
        if(validateForm()){
            if(!prop.data){
                emit("add", [name.value, description.value])
                notify("Task Added!")
                name.value = ""
                description.value = ""
            }else {
                emit("updated", [name.value, description.value, false])
                notify("Task Updated!")
                name.value = ""
                description.value = ""
            }
        }
    }
</script>

<style lang="css" scoped>
    .container .card {
        @media(max-width:600px){
            width: 70vw !important;
        }
        @media(max-width:400px){
            width: 90vw !important;
        }
    }
    .err .form-control  {
        border: 2px solid #d92121;
        position: relative;
    }
    .err:after {
        position: absolute;
        cursor: pointer;
        color:  #d92121;
        content: "Mandatory Field";
    }
</style>

/* Same but with Options API */
/* 
<!--
<template>
<section>
    <h1 v-if="this.data" style="text-align:center">Edit this task</h1>
  <div class="container pt-5 h-100 d-flex justify-content-center align-items-center">
    <div class="card rounded-3" style="width: 60vw;">
        <form class="p-3" @submit.prevent="submitForm">
            <div class="mb-4" :class="{err: checkNameErr}" >
                <label class="form-label" for="form4Example1">Task Name</label>
                <input 
                    type="text" 
                    id="form4Example1" 
                    class="form-control" 
                    v-model="name"
                    @blur="checkErr('name')"
                />
            </div>

            <div class="mb-4" :class="{err: checkDescErr}" >
                <label class="form-label" for="form4Example3">Write a small description...</label>
                <textarea 
                    class="form-control" 
                    id="form4Example3" 
                    rows="2" 
                    v-model="desc" 
                    @blur="checkErr('desc')"
                ></textarea>
            </div>

            <button type="submit" class="btn btn-primary">{{data ? 'Update' : 'Add'}}</button>
        </form>
    </div>
    </div>
    </section>
</template>

<script>
export default {
  name: "TaskForm",
  data(){
    return {
        name: '',
        desc:'',
        error: []
    }
  },
  emits: ['updated','add'],
  props: ['data'],
  mounted() {
    if(this.data){ 
        this.name = this.data.name,
        this.desc = this.data.desc
    }
  },
  computed: {
    checkNameErr(){
        return this.error.includes('nameErr')
    },
    checkDescErr(){
        return this.error.includes('descErr')
    }
  },
  methods: {
    submitForm(){
        this.checkErr('name')
        this.checkErr('desc')
        if(!this.error.length){
            if(!this.data){
                this.$emit("add", [this.name, this.desc])
                this.name = ""
                this.desc = ""
            }else {
                this.$emit("updated", [this.name, this.desc, false])
                this.name = ""
                this.desc = ""
            }
        }
    },
    checkErr(param){
        if(!this[param]){
            if(!this.error.includes(`${param}Err`)){
                this.error.push(`${param}Err`)
            }
        }else {
            const index = this.error.indexOf(`${param}Err`)
            this.error.splice(index)
        }
    }
  }
};
</script>

<style lang="css" scoped>
    .container .card {
        @media(max-width:600px){
            width: 70vw !important;
        }
        @media(max-width:400px){
            width: 90vw !important;
        }
    }
    .err .form-control  {
        border: 2px solid #d92121;
        color: red
    }
    .err:after {
        cursor: pointer;
        color:  #d92121;
        content: "Mandatory Field";
    }
</style>
-->
*/