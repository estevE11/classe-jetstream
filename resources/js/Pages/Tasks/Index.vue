<template>
  <app-layout>
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">Tasks</h2>
    </template>

    <div class="content">
      <div class="max-w-7xl mx-auto py-10 sm:px-6 lg:px-8">
        <update-team-name-form :task="task" :permissions="permissions" />
        <div
          class="task"
          v-for="(task, idx) in tasks"
          :key="task"
          :class="forms[idx].status == 0 ? 'disabled' : 'enabled'"
        >
          <button id="check" @click="updateStatus(idx)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-check"
              viewBox="0 0 16 16"
            >
              <path
                d="M10.97 4.97a.75.75 0 0 1 1.07 1.05l-3.99 4.99a.75.75 0 0 1-1.08.02L4.324 8.384a.75.75 0 1 1 1.06-1.06l2.094 2.093 3.473-4.425a.267.267 0 0 1 .02-.022z"
              />
            </svg>
          </button>
          <h1 id="title">{{ task.title }}</h1>
          <h1 id="description">{{ task.description }}</h1>
          <button id="edit">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-pencil"
              viewBox="0 0 16 16"
            >
              <path
                d="M12.146.146a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1 0 .708l-10 10a.5.5 0 0 1-.168.11l-5 2a.5.5 0 0 1-.65-.65l2-5a.5.5 0 0 1 .11-.168l10-10zM11.207 2.5L13.5 4.793 14.793 3.5 12.5 1.207 11.207 2.5zm1.586 3L10.5 3.207 4 9.707V10h.5a.5.5 0 0 1 .5.5v.5h.5a.5.5 0 0 1 .5.5v.5h.293l6.5-6.5zm-9.761 5.175l-.106.106-1.528 3.821 3.821-1.528.106-.106A.5.5 0 0 1 5 12.5V12h-.5a.5.5 0 0 1-.5-.5V11h-.5a.5.5 0 0 1-.468-.325z"
              />
            </svg>
          </button>
          <button id="thrash" @click="destroy(idx)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-trash"
              viewBox="0 0 16 16"
            >
              <path
                d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"
              />
              <path
                fill-rule="evenodd"
                d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"
              />
            </svg>
          </button>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
    import AppLayout from '@/Layouts/AppLayout'
    import JetSectionBorder from '@/Jetstream/SectionBorder'

    export default {
        props: [
            'tasks',
            'user',
            'availableRoles',
            'permissions',
        ],
        components: {
            AppLayout,
            JetSectionBorder,
        },
        data() {
            return {
                forms: []
            }
        },
        beforeMount() {
            this.init();
        },
        methods: {
            init() {
                const self = this;
                this.tasks.forEach(task => {
                    self.forms.push(self.$inertia.form({
                        status: task.status
                    }));
                });
            },

            updateStatus(i) {
                const self = this;
                this.forms[i].status = !this.forms[i].status;
                this.forms[i].put(route('task.update', this.tasks[i]),
                {
                    errorBag: null,
                });
            },

            destroy(i) {
                const self = this;
                this.forms[i].delete(route('task.destroy', this.tasks[i]),
                {
                    errorBag: null,
                });
            }
        }
    }
</script>

<style scoped>
.content {
  display: flex;
  flex-direction: column;
}
.task {
  display: flex;
  flex-direction: row;
  width: 100vh;
  height: 10vh;
  border-radius: 2vh;
  align-items: center;
}

button{
    outline: none;
}

#thrash{
    height: 10vh;
    width: 10%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1vh;
    margin-right: 1vh;
}

#thrash svg{
    width: 10vh;
    height: 6vh;   
}

#thrash{
    height: 6vh;
}

#thrash svg:hover {
    color: red;    
}

#edit{
    height: 10vh;
    width: 10%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1vh;
    margin-right: 1vh;
}

#edit svg{
    width: 10vh;
    height: 6vh;   
}

#edit{
    height: 6vh;
}

#edit svg:hover {
    color: orange;    
}

#check{
    height: 10vh;
    width: 10%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1vh;
    margin-right: 1vh;
}

#check svg{
    width: 10vh;
    height: 8vh;   
}

#check{
    height: 6vh;
}

#check svg:hover {
    color: rgb(20, 199, 20);    
}


#title{
    height: 10vh;
    width: 20%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1vh;
    margin-right: 1vh;
}

#description{
    height: 10vh;
    width: 40%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1vh;
    margin-right: 1vh;
}
.enabled {
  background-color: rgba(0, 247, 255, 0.6);
}
.disabled {
  background-color: rgba(255, 0, 0, 0.6);
}
</style>